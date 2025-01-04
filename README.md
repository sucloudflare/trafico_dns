# README - Configuração e Execução de Ettercap e Wireshark

## 1. Visão Geral
Este documento descreve como utilizar o **Ettercap** para realizar um ataque ARP e capturar o tráfego de rede, bem como como configurar o **Wireshark** para filtrar pacotes DNS e identificar o nome de sites acessados.

## 2. Pré-requisitos
Antes de executar os comandos, você precisa ter o **Ettercap** e o **Wireshark** instalados em seu sistema. Certifique-se de ter as permissões necessárias (como usuário root) para executar os comandos.

### Instalação do Ettercap
No Debian/Ubuntu, instale o Ettercap com o seguinte comando:

```bash
sudo apt-get install ettercap-text-only

```



### Instalação do Wireshark
Para instalar o Wireshark, utilize:

bash
Copiar código
sudo apt-get install wireshark
3. Usando o Ettercap
O Ettercap é uma ferramenta de segurança que pode ser usada para realizar ataques Man-in-the-Middle (MITM) na rede, como o ataque ARP. O comando para realizar o ataque ARP entre dois IPs específicos e salvar o tráfego é o seguinte:

Comando
bash
Copiar código
sudo ettercap -T -i eth0 -M arp:remote /192.168.10.103/// /192.168.10.1/// --write ./ettercap_log
Explicação do comando:
-T: Modo de execução "text-only" (apenas no terminal).
-i eth0: Especifica a interface de rede (neste caso, eth0).
-M arp:remote: Realiza o ataque ARP remoto entre os IPs especificados.
/192.168.10.103///: Endereço IP de destino (o dispositivo a ser atacado).
/192.168.10.1///: Endereço IP do gateway (roteador).
--write ./ettercap_log: Salva o tráfego de rede capturado no arquivo ettercap_log.




### 4. Filtrando DNS no Wireshark
Para capturar apenas pacotes DNS no Wireshark, utilize o filtro de exibição:

plaintext
Copiar código
dns
Com isso, você conseguirá ver todas as requisições e respostas DNS na rede, incluindo os nomes de domínio que estão sendo acessados.

Exemplo de Pacote DNS:
Consulta DNS (DNS Query):

css
Copiar código
Standard query 0x1234 A example.com
Aqui, example.com é o nome do site que está sendo acessado.

Resposta DNS (DNS Response):

css
Copiar código
192.168.1.1 A 93.184.216.34
Aqui, o domínio example.com foi resolvido para o IP 93.184.216.34.

Como encontrar o nome do site:
Se você observar as requisições DNS (no campo "Queries"), o nome do site será visível como parte da consulta, como example.com.
Nas respostas, você poderá ver o domínio resolvido para o endereço IP.

### 5. Observações
Certifique-se de ter permissão para realizar o ataque ARP, já que ele pode ser utilizado de forma maliciosa.
O Wireshark pode capturar tráfego de sites que usam HTTPS, mas o conteúdo será criptografado. Você pode ver o nome do site nas requisições DNS, mas não o conteúdo da comunicação.
6. Logs e Análise
Após executar o comando do Ettercap, você pode analisar o arquivo de log gerado (por exemplo, ettercap_log) para verificar o tráfego de rede capturado. Esse log pode conter informações sobre os sites acessados, incluindo os endereços IP e os domínios solicitados.


Agora o arquivo está completamente em **Markdown**! Basta salvar com a extensão `.md` para o formato adequado.
