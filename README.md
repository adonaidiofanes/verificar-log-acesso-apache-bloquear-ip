verificar-log-acesso-apache-bloquear-ip
=======================================

Verificar IPS que atacam pelo log de acesso do apache, bloquear esses IPs com IPTABLES

#!/bin/bash

echo "===> Entre com o IP a ser verificado :) <==="

read ipVerificar

echo ""

echo "===> Verificando IP <==="
echo ""

cat /var/log/apache2/access.log |grep $ipVerificar > /root/logAtaque.txt

echo "========================================"
echo "============= RELATORIO ================"
echo "========================================"
echo "===[ IP: $ipVerificar ]================="
echo "==== QUANTIDADE DE LINHAS  ENCONTRADAS: "
echo "========================================"
wc -l /root/logAtaque.txt
echo "========================================"
echo ""
echo ""

echo "===> Você deseja bloquear o IP $ipVerificar [s/n]?"

read varBloquear
echo ""
echo ""
echo "A opção foi $varBloquear"


if [ $varBloquear = "s" ]; then
   echo ""
   echo "=> BLOQUEANDO IP"
   iptables -I INPUT -s $ipVerificar -j DROP
   echo "IP BLOQUEADO"
else
   echo "Script finalizado!"	
fi



