在Android5.1代码中,网络的优先级是wifi>ethernet>data
```
diff --git a/frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetNetworkFactory.java b/frameworks/opt/net/ethernet/java/com/an
index 1248ccf..cfd6ccf 100644
--- a/frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetNetworkFactory.java
+++ b/frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetNetworkFactory.java
@@ -71,7 +71,7 @@ import java.io.PrintWriter;
 class EthernetNetworkFactory {
     private static final String NETWORK_TYPE = "Ethernet";
     private static final String TAG = "EthernetNetworkFactory";
-    private static final int NETWORK_SCORE = 70;
+    private static final int NETWORK_SCORE = 150;
     private static final boolean DBG = true;
 
     /** Tracks interface changes. Called from NetworkManagementService. */
```

修改成150是因为wifi的score最高是100 。