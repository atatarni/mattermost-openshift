# Mattermost for OpenShift Enterprise 3

This is instant mattermost application for OpenShift Enterprise 3. There is also
an OpenShift Origin flavor on the centos7 branch.

The license applies to all files insinde this repository, not mattermost itself.

## Prerequisites

OpenShift Enterprise 3 up and running, including the capability to create a new project.


## Installation

```
oc new-project mattermost
oc project mattermost
oc new-app -f https://raw.githubusercontent.com/goern/mattermost-openshift/mattermost.yaml
```

You need to provision a PV:
```
# cat mattermost-pv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  nfs:
    path: /srv/nfs/path
    server: nfs-server
  persistentVolumeReclaimPolicy: Retain

# oc create -f mattermost-pv.yaml
```

and a route:

`oc expose service/mattermost --hostname=mattermost.example.com`


## Usage

Point your browser at `mattermost.example.com`, the first user you create will
be an Administrator of mattermost.


## Copyright

Copyright (C) 2016 Red Hat Inc.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.

The GNU General Public License is provided within the file LICENSE.
