# OLT-V-SOL-GPON

Importe o template https://github.com/gabrielteixeiranetwork/OLT-V-SOL-GPON/blob/main/OLT%20VSOL%20GPON%20COMPLETO.xml

Entre no seu zabbix via ssh na pasta /usr/lib/zabbix/externalscripts/ cria o arquivo onus_offlines

Feito isso entre em onus_offlines e adicione o script

    #!/bin/bash

    COMMUNITY=$1
    IP=$2

    # Total autorizadas
    aut=$(snmpwalk -v2c -c $COMMUNITY $IP 1.3.6.1.4.1.37950.1.1.6.1.1.18.1.2 | awk '{print $4}' | awk '{soma+=$1} END {print soma}')

    # Total onlines
    onl=$(snmpwalk -v2c -c $COMMUNITY $IP 1.3.6.1.4.1.37950.1.1.6.1.1.18.1.3 | awk '{print $4}' | awk '{soma+=$1} END {print soma}')

    # Total offlines
    off=$((aut-onl))

    echo $off
    
Importe a Dashboard para o grafana e sucesso  :)
