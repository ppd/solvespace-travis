# solvespace-travis

##  Cfg for remote-build

1. Create ssh key for git.launchpad.net (add to launchpad)
2. Create launchpad credentials by running ```snapcraft remote-build --user <user>``` locally
3. Pack secrets together:

```bash
cp ~/.local/share/snapcraft/launchpad/credentials launchpad-credentials
cp ... remote-build-key
tar cvf secrets.key launchpad-credentials remote-build-key
```
4. Push secrets to Travis: ```travis encrypt-file secrets.key```
5. Add openssl command to .travis.yml

## Cfg for deploy stage

```bash
snapcraft export-login --snaps=solvespace --channels=edge snapcraft-login
travis env set SNAP_TOKEN "$(cat snapcraft-login)"
```
