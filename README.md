# lesson11
# standalone
repo: https://yum.puppetlabs.com/puppetlabs-release-pc1-el-6.noarch.rpm

**create manifest with content:**

```
package { 'nginx':
        ensure=>'installed'
}

notify { 'Nginx is installed.':
}

service { 'nginx':
        ensure=>'running'
}

notify { 'Nginx is running.':
}
```
run command: ***puppet apply /path_to_file/***

![im](https://github.com/alekskar/lesson11/blob/master/res/pup_standalone.png)

check that nginx get correct responce code:

![im](https://github.com/alekskar/lesson11/blob/master/res/pup_200ok_stand.png)
# client master
### on client mashine:
```
  - service puppet start
  - puppet agent --server puppetserver.minsk.epam.com --waitforcert 60 --test
```

![im](https://github.com/alekskar/lesson11/blob/master/res/pup_node_cert.png)

# on master server:
```
puppet cert --list
pupper cert --sign puppetstandalone.minsk.epam.com
puppet module install puppetlabs-ntp
```
![im](https://github.com/alekskar/lesson11/blob/master/res/pup_serv_cert.png)

create file 
```
vi /etc/puppetlabs/code/environments/production/manifests/site.pp
```
with content:
```

node puppetstandalone.minsk.epam.com {
  class { 'ntp':
  servers => ['0.by.pool.ntp.org','2.europe.pool.ntp.org']
  }
}
```
run command to forse pull data from server:
```
puppet agent --server puppetserver.minsk.epam.com -t
```
![im](https://github.com/alekskar/lesson11/blob/master/res/pup_ntp_module.png)


