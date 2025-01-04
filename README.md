<h1>README - Configuração e Execução de Ettercap e Wireshark</h1>

<h2>1. Visão Geral</h2>
<p>Este documento descreve como utilizar o <strong>Ettercap</strong> para realizar um ataque ARP e capturar o tráfego de rede, bem como como configurar o <strong>Wireshark</strong> para filtrar pacotes DNS e identificar o nome de sites acessados.</p>

<h2>2. Pré-requisitos</h2>
<p>Antes de executar os comandos, você precisa ter o <strong>Ettercap</strong> e o <strong>Wireshark</strong> instalados em seu sistema. Certifique-se de ter as permissões necessárias (como usuário root) para executar os comandos.</p>

<h3>Instalação do Ettercap</h3>
<p>No Debian/Ubuntu, instale o Ettercap com o seguinte comando:</p>
<pre><code>sudo apt-get install ettercap-text-only</code></pre>

<h3>Instalação do Wireshark</h3>
<p>Para instalar o Wireshark, utilize:</p>
<pre><code>sudo apt-get install wireshark</code></pre>

<h2>3. Usando o Ettercap</h2>
<p>O <strong>Ettercap</strong> é uma ferramenta de segurança que pode ser usada para realizar ataques Man-in-the-Middle (MITM) na rede, como o ataque ARP. O comando para realizar o ataque ARP entre dois IPs específicos e salvar o tráfego é o seguinte:</p>

<h3>Comando</h3>
<pre><code>sudo ettercap -T -i eth0 -M arp:remote /192.168.10.103/// /192.168.10.1/// --write ./ettercap_log</code></pre>

<h3>Explicação do comando:</h3>
<ul>
<li><code>-T</code>: Modo de execução "text-only" (apenas no terminal).</li>
<li><code>-i eth0</code>: Especifica a interface de rede (neste caso, <code>eth0</code>).</li>
<li><code>-M arp:remote</code>: Realiza o ataque ARP remoto entre os IPs especificados.</li>
<li><code>/192.168.10.103///</code>: Endereço IP de destino (o dispositivo a ser atacado).</li>
<li><code>/192.168.10.1///</code>: Endereço IP do gateway (roteador).</li>
<li><code>--write ./ettercap_log</code>: Salva o tráfego de rede capturado no arquivo <code>ettercap_log</code>.</li>
    </ul>

<h2>4. Filtrando DNS no Wireshark</h2>
<p>Para capturar apenas pacotes DNS no <strong>Wireshark</strong>, utilize o filtro de exibição:</p>
<pre><code>dns</code></pre>
<p>Com isso, você conseguirá ver todas as requisições e respostas DNS na rede, incluindo os nomes de domínio que estão sendo acessados.</p>

<h3>Exemplo de Pacote DNS:</h3>
<ul>
<li><strong>Consulta DNS (DNS Query):</strong>
<pre><code>Standard query 0x1234 A example.com</code></pre>
            Aqui, <code>example.com</code> é o nome do site que está sendo acessado.
</li>
<li><strong>Resposta DNS (DNS Response):</strong>
<pre><code>192.168.1.1 A 93.184.216.34</code></pre>
            Aqui, o domínio <code>example.com</code> foi resolvido para o IP <code>93.184.216.34</code>.
</li>
</ul>

<h3>Como encontrar o nome do site:</h3>
<ul>
  <li>Se você observar as requisições DNS (no campo "Queries"), o nome do site será visível como parte da consulta, como <code>example.com</code>.</li>
<li>Nas respostas, você poderá ver o domínio resolvido para o endereço IP.</li>
</ul>

<h2>5. Observações</h2>
<ul>
<li>Certifique-se de ter permissão para realizar o ataque ARP, já que ele pode ser utilizado de forma maliciosa.</li>
<li>O Wireshark pode capturar tráfego de sites que usam HTTPS, mas o conteúdo será criptografado. Você pode ver o nome do site nas requisições DNS, mas não o conteúdo da comunicação.</li>
</ul>

<h2>6. Logs e Análise</h2>
<p>Após executar o comando do <strong>Ettercap</strong>, você pode analisar o arquivo de log gerado (por exemplo, <code>ettercap_log</code>) para verificar o tráfego de rede capturado. Esse log pode conter informações sobre os sites acessados, incluindo os endereços IP e os domínios solicitados.</p>
