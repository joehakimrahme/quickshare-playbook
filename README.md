Quick Share Playbook
====================

This is an Ansible playbook that deploys a simple FTP server on a single
node. I use it to share large files with friends.

Quickstart
----------

1. Before you start, make sure to get SSH access to the root user of a remote
   server running CentOS 7. You also need to have [Ansible](http://ansible.com)
   installed locally.

2. Clone this playbook locally:

```
    $ git clone https://github.com/joehakimrahme/quickshare-playbook.git
```

3. Copy the file you want to share

```
    $ cp "$my_file" roles/ftp/files/
```
    
4. Fill out the options in `group_vars/all`.

5. Create a host file (you can copy the `host.sample` or simply have a `hosts`
   file with just one line).

6. Execute the playbook.

```
    $ ansible-playbooks -i hosts site.yml
```


That's it, your file is now available at the following address:
`ftp://$YOUR_IP/pub/$my_file`.


Some notes
----------

1. It's possible to configure vsftp to accept anonymous uploads. It's also
   possible to require a username/password. This can be controlled in the
   `group_vars/all` file.
   
2. While not necessary, it's **highly recommended** that you deploy this
   playbook on a discardable fresh node. The way I do it is to boot a new VM on
   a cloud provider, deploy this playbook then destroy the VM as soon as the
   recipient has retrieved the file.
   
3. The playbook should work (but hasn't been tested) on any RHEL/CentOS recent
   version, and to a lesser extent, Fedora.

4. Remember that your recipient doesn't need a fancy FTP client to get the file
   since most modern web browsers also support this protocol. And here's a quick
   reminder that even [curl can FTP](http://rahme.info/curl-can-ftp).
