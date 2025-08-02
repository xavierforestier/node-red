# node-red
This repo is a placeholder to store nodes_modules dependencies for gentoo ebuild app-misc/node-red

## How to create a new node-red version

### Create a temporary ebuild for new version a.b.c
Enter your repo and copy last version x.y.z ebuild to the new version :
```bash
cd /var/db/repos/xxx/app-misc/node-red
cp node-red-x.y.z.ebuild node-red-a.b.c.ebuild
```

Now edit new ebuild and comment nodes_modules.tar.xz part in SRC_URI (line 11)
Unpack the source :
```bash
ebuild node-red-a.b.c.ebuild digest clean unpack
```

Go in the extracted source, generate nodes_modules :
```bash
pushd /var/tmp/portage/app-misc/node-red-a.b.c/work/node-red-a.b.c
npm install
```
Generate nodes_module-a.b.c.tar.xz
```bash
pushd ..
XZ_OPT=-9 tar -Jcvf node-red-a.b.c-nodes_modules.tar.xz node-red-a.b.c/node_modules/
```

Upload node_modules in a release tagged a.b.c
