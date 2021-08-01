
- build code 下 -fetch 就把家裡網路癱瘓的, 可以這樣改 eos_build
  - user smaller -j "parser.add_argument("-j", type=int, **default=8,** help="Specify number of simultaneous Jobs.  Default is num cpus")"
```
diff --git a/scripts/getpkgs.py b/scripts/getpkgs.py
index 610c284..c41f1ae 100644
--- a/scripts/getpkgs.py
+++ b/scripts/getpkgs.py
@@ -288,7 +288,7 @@ parser.add_argument('-f','--filter', nargs='*', help='List of filter tags that t
 parser.add_argument('-a','--archs', nargs='*', help='List of filter architectures that this fetch will support')
 parser.add_argument('--cache', help='Path to artifact cache to use')
 parser.add_argument('--cachesize', help='Artifact cache max size in MB, default 32768', type=int, default=32768)
-#parser.add_argument("-j", type=int, default=os.cpu_count(), help="Specify number of simultaneous Jobs.  Default is num cpus")
+parser.add_argument("-j", type=int, default=8, help="Specify number of simultaneous Jobs.  Default is num cpus")
 args = parser.parse_args()
```