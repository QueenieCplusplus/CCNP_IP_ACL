# CCNP IP ACL
IP Access Lists


# IP Standard Access List 標準存取列表

* 常用指令：

        access-list 存取列表

        acess-list-number 存取列表號碼（預設為 1-99, 延伸號碼為 100-199）

        permit 允許

        deny 拒絕

        Source 來源IP位址

        Source-wildcard 來源的運算位元

        any 任何位置，代表 Source address 0.0.0.0 和 Source-wildcard 255.255.255.255

* 指令語法

          #access-list + list-number + permit or deny + tcp or udp or icmp + 
           src addr + wildcard + src port +
           des addr + wildcard + des port
          


# IP Extended Access List 延伸存取列表

* 延伸目的

提供 SMTP 和 DNS 的服務

* 實際意象

        10.64.0.2
          Server.  ------------- 10.64.0.0 - E0 - Router - S0 - --------    Internet
          


* 實作範例


           R(config)#access-list 130 permit tcp any host 10.64.0.2 eq smtp
           R(config)#access-list 130 permit udp any eq domain any
           R(config)#int s0
           R(config-if)#ip access-group 130 in


# Null int 空介面

* 存在目的

單純限制網路封包走向，且不耗損 CPU 的存取控制方式。
只要指定封包至此介面，便等同丟棄 drop 封包。

* 指令語法

                 #ip route + < des addr > + < mask > + int
            

* 實作範例

            // 空介面的編號是 null 0
            // 將送往 203.66.47.0 的封包丟棄

            R(config)#ip route 203.66.47.0 255.255.255.0 null 0


