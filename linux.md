













<details> <summary>Users and Groups</summary>

```
useradd -r -s /bin/false exampleSysUser # Create a fake system user for programs. Don't allow shell connection
useradd -m -d /home/exampleUser         # Create a user with a home directory
```



1. Owner
2. Group
3. Public

Read  | Write | Execute 
------|-------|-------
4 | 2 | 1

Examples: </br>
111 = `--x--x--x` </br>
333 = `-wx-wx-wx`</br>





</summary> </details>



<details> <summary>Systemd</summary>




## Create a bash script to run on boot up

1. Create the script at `/usr/local/sbin/example-script.sh`
- Change permissions `chmod +x example-script.sh`

2. Create file `/etc/systemd/system/example-script.service` with contents:
```
[Unit]
Description=Start Me At Bootup

[Service]
ExecStart=/usr/local/sbin/example-script.sh

[Install]
WantedBy=multi-user.target
```
3. Enable the service so it runs on boot up
`systemctl enable example-script.service'

</summary> </details>

