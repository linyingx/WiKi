以下代码需要应用具有系统权限, 并且支持有网络.

且此代码基于惠尔丰X990(Android5.1)开发,系统是定制系统,可能不适用于别的机型.

```
package com.xd.devicepolicymanager;

import android.annotation.TargetApi;
import android.app.Service;
import android.content.Context;
import android.content.Intent;
import android.net.LinkAddress;
import android.net.ProxyInfo;
import android.os.Build;
import android.os.IBinder;
import android.util.Log;
import android.widget.Toast;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Type;
import java.net.Inet4Address;
import java.net.InetAddress;
import java.util.ArrayList;

public class AdbDebugService extends Service {

    private String TAG = "EthernetTest";

    @Override
    public void onCreate() {
        super.onCreate();
        Toast.makeText(this, "Service created...", Toast.LENGTH_LONG).show();
    }

    @TargetApi(Build.VERSION_CODES.LOLLIPOP)
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        try {
            Class<?> EthernetManagerCls = Class.forName("android.net.EthernetManager");
            Class<?> IpConfigurationCls = Class.forName("android.net.IpConfiguration");
            Class<?> StaticIpConfigurationCls = Class.forName("android.net.StaticIpConfiguration");
            Class<?> NetworkUtilsCls = Class.forName("android.net.NetworkUtils");
            Class<?> ContextCls = Class.forName("android.content.Context");
            Class<?> LinkAddressCls = Class.forName("android.net.LinkAddress");
            Class<?> IpAssignmentCls = Class.forName("android.net.IpConfiguration$IpAssignment");
            Class<?> ProxySettingsCls = Class.forName("android.net.IpConfiguration$ProxySettings");

            Method getConfigurationMethod = null;
            Method setConfigurationMethod = null;

            Object EthernetManagerObj = null;
            Object LinkAddressObj = null;
            Object IpConfiguationObj = null;
            Object StaticIpConfigurationObj = StaticIpConfigurationCls.newInstance();

            Method mths[] = EthernetManagerCls.getDeclaredMethods();
            for (Method m : mths) {
                if (m.getName().equals("setConfiguration"))
                    setConfigurationMethod = m;
                if (m.getName().equals("getConfiguration"))
                    getConfigurationMethod = m;
            }
            if (setConfigurationMethod == null | getConfigurationMethod == null) {
                Toast.makeText(this, "error2", Toast.LENGTH_LONG).show();
            }

            try {
                //get Ethernet SystemService
                EthernetManagerObj = ContextCls.getDeclaredMethod(
                        "getSystemService", String.class)
                        .invoke(this, "ethernet");

                Inet4Address inetAddr = (Inet4Address) NetworkUtilsCls.getDeclaredMethod(
                        "numericToInetAddress", String.class)
                        .invoke(null, "192.168.2.104");
                Inet4Address gatewayAddr = (Inet4Address) NetworkUtilsCls.getDeclaredMethod(
                        "numericToInetAddress", String.class)
                        .invoke(null, "255.255.255.0");
                Inet4Address dnsAddr = (Inet4Address) NetworkUtilsCls.getDeclaredMethod(
                        "numericToInetAddress", String.class)
                        .invoke(null, "192.168.2.1");

                LinkAddressObj = LinkAddressCls.getDeclaredConstructor(
                        InetAddress.class, int.class)
                        .newInstance(inetAddr, 24);

                StaticIpConfigurationCls.getField("ipAddress").set(StaticIpConfigurationObj, LinkAddressObj);
                StaticIpConfigurationCls.getField("gateway").set(StaticIpConfigurationObj, gatewayAddr);
                ArrayList<Inet4Address> dnsServers = (ArrayList<Inet4Address>) (StaticIpConfigurationCls
                        .getField("dnsServers").get(StaticIpConfigurationObj));
                dnsServers.add(dnsAddr);

                Constructor<?>[] constructors = IpConfigurationCls.getConstructors();
                for (Constructor<?> cons : constructors) {
                    if (cons.getGenericParameterTypes().length == 4) {
                        IpConfiguationObj = cons.newInstance(
                                IpAssignmentCls.getField("STATIC").get(null),
                                ProxySettingsCls.getField("NONE").get(null),
                                StaticIpConfigurationObj, null);
                        break;
                    }
                }
            } catch (NoSuchMethodException e) {
                e.printStackTrace();
                Toast.makeText(this, "error6", Toast.LENGTH_LONG).show();
            } catch (NoSuchFieldException e) {
                Toast.makeText(this, "error7", Toast.LENGTH_LONG).show();
                e.printStackTrace();
            }

            setConfigurationMethod.invoke(EthernetManagerObj, IpConfiguationObj);

            IpConfiguationObj = getConfigurationMethod.invoke(EthernetManagerObj);

            Object isAssignment = IpConfigurationCls.getField("ipAssignment").get(IpConfiguationObj);
            if (isAssignment != IpAssignmentCls.getField("STATIC").get(null)) {
                Toast.makeText(this, "Static IP setup failed!", Toast.LENGTH_LONG).show();
            }


        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            Toast.makeText(this, "error1", Toast.LENGTH_LONG).show();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
            Toast.makeText(this, "error3", Toast.LENGTH_LONG).show();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
            Toast.makeText(this, "error4", Toast.LENGTH_LONG).show();
        } catch (InstantiationException e) {
            e.printStackTrace();
            Toast.makeText(this, "error5", Toast.LENGTH_LONG).show();
        } catch (NoSuchFieldException e) {
            e.printStackTrace();
            Toast.makeText(this, "error9", Toast.LENGTH_LONG).show();
        }
        Toast.makeText(this, "Service onStartCommand...", Toast.LENGTH_LONG).show();

        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Toast.makeText(this, "Service destroyed...", Toast.LENGTH_LONG).show();
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```