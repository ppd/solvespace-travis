# solvespace-travis

##  Cfg for remote-build

1. Create ssh key for git.launchpad.net (add to launchpad)
2. Create launchpad credentials by running ```snapcraft remote-build --user <user>``` locally
3. Pack secrets together:

```bash
cp ~/.local/share/snapcraft/launchpad/credentials launchpad-credentials
cp ... remote-build-key
tar cvf secrets.tar launchpad-credentials remote-build-key
```
4. Push secrets to Travis: ```travis encrypt-file secrets.tar```
5. Add openssl command to .travis.yml

Snapcraft/launchpad will gain support for submitting builds without the use of a ssh key in the near (?) future.

## Cfg for deploy stage

```bash
snapcraft export-login --snaps=solvespace --channels=edge snapcraft-login
travis env set SNAP_TOKEN "$(cat snapcraft-login)"
```

## Build logs

For launchpad user ```lpuser```: https://code.launchpad.net/~lpuser/+snap/
