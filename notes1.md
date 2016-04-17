## Building a basic RPM package

```bash
yum install rpmdevtools
# as non-root user:
rpmdev-setuptree
mkdir example-1.0
echo "Here is some text." > example-1.0/example-file.txt
tar czf example-1.0.tar.gz example-1.0
cp example-1.0.tar.gz rpmbuild/SOURCES
rpmdev-newspec rpmbuild/SPECS/example.spec
# edit rpmbuild/SPECS/example.spec accordingly
# see: example.spec
rpmbuild -ba rpmbuild/SPECS/example.spec
```
