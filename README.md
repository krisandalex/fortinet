# fortinet

#https://community.fortinet.com/t5/FortiGate/Technical-Note-Log-message-ignoring-request-to-establish-IPsec/ta-p/198467

#ipsec route based configuration 

config system interface
    edit "AsaFP.22"
        set vdom "root"
        set ip 192.168.254.10 255.255.255.255
        set type tunnel
        set remote-ip 192.168.254.9 255.255.255.0
        set snmp-index 17
        set mtu-override enable
        set mtu 1300
        set interface "wan1"
    next
end

config vpn ipsec phase1-interface
    edit "AsaFP.22"
        set interface "wan1"
        set ike-version 2
        set peertype any
        set net-device disable
        set proposal des-sha1 des-sha256 chacha20poly1305-prfsha1 aes256gcm-prfsha384 chacha20poly1305-prfsha256 des-sha384 des-sha512
        set remote-gw <IPREMOTEPEER>
        set psksecret ENC bla bla bla
    next
end
config vpn ipsec phase2-interface
    edit "AsaFP.22"
        set phase1name "AsaFP.22"
        set proposal des-sha1 des-sha512 des-sha256 des-sha384
        set dhgrp 5 2
    next
end

*****AND set route at both place to needed net*****


