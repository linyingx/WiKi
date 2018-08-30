```
import commands
cmd = ("build_verity_tree -A %s %s %s" % (FIXED_SALT, sparse_image_path, verity_image_path))
status, output = commands.getstatusoutput(cmd)
```

```
#!/usr/bin/env python
#python 脚本都需要加这一行
 
 import commands
 import sys 
 
 FIXED_SALT = "aee087a5be3b982978c923f566a94613496b417f2af592639bc80d141e34dfe7"
 
 def BuildVerityTree1(sparse_image_path, verity_image_path):
   cmd = ("build_verity_tree -A %s %s %s" % (FIXED_SALT, sparse_image_path, verity_image_path))
   print cmd 
   status, output = commands.getstatusoutput(cmd)
   if status:
     print "Could not build verity tree! Error: %s" % output
     return False
   root, salt = output.split()
   print "%s" % output
   return True
 
 def main(argv):
   if len(argv) != 1:
     print __doc__
     sys.exit(1)
 
   out_file = argv[0]
 
   BuildVerityTree1(out_file, "verity.img")
   exit(1)
 
 #调用main 及 使用参数
 if __name__ == '__main__':
   main(sys.argv[1:])
```