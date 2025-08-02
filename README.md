# nodes-red
This repo is a placeholder to store nodes_modules dependencies for gentoo ebuild app-misc/nodes-red

## How to create a new nodes-red version

### Create a temporary ebuild for new version a.b.c
Enter your repo and copy last version x.y.z ebuild to the new version :
```bash
cd /var/db/repos/xxx/app-misc/nodes-red
cp nodes-red-x.y.z.ebuild nodes-red-a.b.c.ebuild
```

Now edit new ebuild and comment nodes_modules.tar.xz part in SRC_URI (line 11)
Unpack the source :
```bash
ebuild nodes-red-a.b.c.ebuild digest clean unpack
```

Go in the extracted source, generate nodes_modules :
```bash
pushd /var/tmp/portage/app-misc/nodes-red-a.b.c/work/nodes-red-a.b.c
npm install
```
Generate nodes_module-a.b.c.tar.xz
```bash
pushd ..
XZ_OPT=-9 tar -Jcvf nodes-red-a.b.c-nodes_modules.tar.xz nodes-red-a.b.c/node_modules/
```

Upload node_modules in a release tagged a.b.c
