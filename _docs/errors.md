# Ubuntu USB ethernet error : "activation of network connection failed"
  ```
  $ ifconfig
  $ iwconfig
  $ sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
    >> [connection]
        wifi.powersave = 3 -> 2
  ```
  ref : https://easylinuxtipsproject.blogspot.com/p/internet.html#ID2.1
        https://easylinuxtipsproject.blogspot.com/p/copy-paste.html
