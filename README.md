# Ansible Role: S3fs

Ansible Role that installs and configure s3fs on Redhat/CentOS 7. Aditionally, install a start/stop script to mount/unmount buckets and add the mountpoints to the fstab file.


# Play
```site.yaml
---
- hosts: localhost
- hosts: phonethingee
  roles:
    - role: ../roles/s3fs
      s3fs:
        source: "https://github.com/s3fs-fuse/s3fs-fuse/archive/v1.78.tar.gz"
        buckets:
          - mountpoint: /mnt/mys3bucket1
            bucket: ""
            accessKeyId: ""
            secretAccessKey: ""
            options: "allow_other,use_cache=/tmp/cache,max_stat_cache_size=100000,uid=33,gid=33,umask=002"
        buckets:
          - mountpoint: /mnt/mys3bucket2
            bucket: ""
            accessKeyId: ""
            secretAccessKey: ""
            options: "allow_other,use_cache=/tmp/cache,max_stat_cache_size=100000,uid=33,gid=33,umask=002"
        add_to_fstab: True
        passwd_file: /etc/passwd-s3fs
        daemon: /usr/local/bin/s3fs
        dependencies:
          - "automake"
          - "fuse"
          - "fuse-devel"
          - "gcc-c++"
          - "git"
          - "libcurl-devel"
          - "libxml2-devel"
          - "make"
          - "openssl-devel"
```