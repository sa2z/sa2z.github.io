# Ubuntu USB ethernet error : "activation of network connection failed"
  ```
  $ ifconfig
  $ inxi -Fxz
  $ iwconfig
  $ sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
    >> [connection]
        wifi.powersave = 3 -> 2
  $ service networking restart
  $ systemctl restart network
  $ systemctl restart NetworkManager
  $ nmcli connection up 'adapter name'
  $ dhclinet
  $ sudo iwconfig wlp6s0 txpower 18
  # state
  $ sudo gedit /var/lib/NetworkManager/NetworkManager.state
  
  # restart
  $ sudo service network-manager stop/start
  ```
  ref : https://easylinuxtipsproject.blogspot.com/p/internet.html#ID2.1
        https://easylinuxtipsproject.blogspot.com/p/copy-paste.html
