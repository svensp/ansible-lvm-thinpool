VerosK.lvm-thinpool
=========

This role sets up LVM thin pool on a defined VG. The thin pool is commonly used to host Docker 
storage.

Role Variables
--------------

Use list `lvm_thinpools`.  This list contain dictionary of each thin pool setting.


     lvm_thinpools:
          - name: thinpool                # name of the thin pool LV
	    volume_group: docker          # VG holding that LV
	    physical_volumes:	          # the VG will be created when this key is defined
	      - /dev/disk/by-id/ata-VIRTUAL_docker 
	    metadata_size: "1%VG"         # size of metadata
	    data_size: "90%VG"            # size of data pool


Example Playbook
----------------
  
    - hosts: servers
      vars:
        lvm_thinpools:
          - name: thinpool
	    volume_group: docker
	    physical_volumes:
	      - /dev/disk/by-id/ata-VIRTUAL_docker
	    metadata_size: "1%VG"
	    data_size: "90%VG"

      roles:
         - role: VerosK.lvm-thinpool

Tested on CentOS 7, should probably work on other modern Linux system too.

License
-------

BSD

Author Information
------------------

VerosK < https://github.com/verosk >

Role development sponsored by Twisto.cz
