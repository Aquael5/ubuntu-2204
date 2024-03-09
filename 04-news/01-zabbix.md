#Autor: Robson Vaamonde<br>
#Procedimentos em TI: http://procedimentosemti.com.br<br>
#Bora para Prática: http://boraparapratica.com.br<br>
#Robson Vaamonde: http://vaamonde.com.br<br>
#Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi<br>
#Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica<br>
#Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem<br>
#YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica<br>
#Data de criação: 07/03/2024<br>
#Data de atualização: 09/03/2024<br>
#Versão: 0.04<br>

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO ZABBIX SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do Zabbix realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/11-zabbix.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiozabbix

Conteúdo estudado nesse desafio:<br>
#01_ Instalando as Dependências do Zabbix Server e Agent<br>
#02_ Adicionando o Repositório do Zabbixn no Ubuntu Server<br>
#03_ Instalando o Zabbix Server, Frontend e Agent<br>
#04_ Criando a Base de Dados no MySQL Server do Zabbix Server<br>
#05_ Testando o acesso a Base de Dados no MySQL Server do Zabbix Server<br>
#06_ Populando as Tabelas no Banco de Dados do Zabbix Server<br>
#07_ Editando os arquivos de Configurações do Zabbix Server e Agent<br>
#08_ Habilitando o Serviço do Zabbix Server e Agent<br>
#09_ Verificando o Serviço e Versão do Zabbix Server e Agent<br>
#10_ Configurando o Zabbix Server via Navegador<br>
#11_ Verificando a Porta de Conexão do Zabbix Server e Agent<br>
#12_ Localização dos diretórios principais do Zabbix Server e Agent<br>
#13_ Instalando os Agentes do Zabbix no Linux Mint e no Windows 10<br>
#14_ Criando os Hosts de Monitoramento dos Agentes no Zabbix Server<br>

Site Oficial do Zabbix: https://www.zabbix.com/<br>

Traduzido do inglês-O Zabbix é uma ferramenta de software de código aberto para monitorar<br>
a infraestrutura de TI, como redes, servidores, máquinas virtuais e serviços em nuvem. O <br>
Zabbix coleta e exibe métricas básicas.

[![Zabbix](http://img.youtube.com/vi//0.jpg)]( "Zabbix")

Link da vídeo aula: 

#01_ Instalando as Dependências do Zabbix Server e Agent<br>

	#atualizando as lista do apt
	sudo apt update

	#instalando as dependências do Zabbix
	sudo apt install traceroute nmap snmp snmpd snmp-mibs-downloader apt-transport-https \
	software-properties-common git vim fping

#02_ Adicionando o Repositório do Zabbix no Ubuntu Server<br>

	#Link de referência do download: https://www.zabbix.com/download
	
	#OBSERVAÇÃO IMPORTANTE: NESSE VÍDEO ESTÁ SENDO INSTALADO E CONFIGURADO A VERSÃO 7.0
	#PRE-RELEASE (BETA - NÃO OFICIAL LTS), A VERSÃO LTS (Long Time Support) É: 6.4.

	#OBSERVAÇÃO IMPORTANTE: NAS CONFIGURAÇÕES DE DOWNLOAD DO REPOSITÓRIO DO ZABBIX SERVER
	#FOI SELECIONADO: 7.0 PRE-RELEASE, Ubuntu, 22.04 (Jammy), Server, Frontend, Agent, MySQL
	#e Apache.

	#download do repositório do Zabbix Server
	wget https://repo.zabbix.com/zabbix/6.5/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.5-1+ubuntu22.04_all.deb

	#instalação do repositório do Zabbix Server
	#opção do comando dpkg: -i (install)
	sudo dpkg -i zabbix-release_6.5*.deb

#03_ Instalando o Zabbix Server, Frontend e Agent<br>

	#OBSERVAÇÃO IMPORTANTE: para a instalação do Zabbix Server e necessário ter instalado e
	#configurado de forma correto o MySQL Server e o Apache2 Server, no caso do Banco de Dados
	#MySQL Server pode ficar em outro servidor (Recomendado).

	#atualizando as lista do apt com o novo repositório do Zabbix
	sudo apt update

	#instalando o Zabbix
	#opção do comando apt: --install-recommends (Consider suggested packages as a dependency for installing)
	sudo apt install --install-recommends zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf \
	zabbix-sql-scripts zabbix-agent

#04_ Criando a Base de Dados no MySQL Server do Zabbix Server<br>

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u root -p

```sql
/* Criando o Banco de Dados Zabbix */
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;

/* Criando o Usuário Zabbix com a Senha Zabbix do Banco de Dados Zabbix */
CREATE USER 'zabbix'@'localhost' IDENTIFIED WITH mysql_native_password BY 'zabbix';
GRANT USAGE ON *.* TO 'zabbix'@'localhost';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;

/* Habilitando a opção de Criação de Função log_bin_trust_function_creators no MySQL Server */
SET GLOBAL log_bin_trust_function_creators = 1;

/* Listando os Bancos de Dados do MySQL */
SHOW DATABASES;

/* Verificando o Usuário Zabbix criado no Banco de Dados MySQL Server */
SELECT user,host FROM mysql.user WHERE user='zabbix';

/* Saindo do Banco de Dados */
exit
```

#05_ Testando o acesso a Base de Dados no MySQL Server do Zabbix Server<br>

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u zabbix -p

```sql
/* Listando os Bancos de Dados do MySQL */
SHOW DATABASES;

/* Acessando o Banco de Dados Zabbix */
USE zabbix;

/* Saindo do Banco de Dados */
exit
```

#06_ Populando as Tabelas no Banco de Dados do Zabbix Server utilizando o arquivo de Esquema<br>

	#OBSERVAÇÃO IMPORTANTE: ESSE PROCESSO DEMORA UM POUCO DEPENDENDO DO SEU HARDWARE

	#importando o esquema e os dados iniciais do banco de dados do Zabbix
	#opções do comando mysql: -u (user), -p (password), zabbix (database)
	sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | sudo mysql --default-character-set=utf8mb4 \
	-uzabbix -pzabbix zabbix 

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u zabbix -p

```sql
/* Acessando o Banco de Dados Zabbix */
USE zabbix;

/* Verificando as Tabelas criadas pelo Script */
SHOW TABLES;

/* Verificando os Usuários criados pelo Script */
SELECT username,passwd FROM users;

/* Saindo do Banco de Dados */
exit
```

	#Desabilitando a opção de Criação de Função no MySQL Server

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u root -p

```sql
/* Desabilitando a opção de Criação de Função log_bin_trust_function_creators no MySQL Server */
SET GLOBAL log_bin_trust_function_creators = 0;

/* Saindo do Banco de Dados */
exit
```

#07_ Editando os arquivos de Configurações do Zabbix Server e Agent<br>

	#editando o arquivo de configuração do Zabbix Server
	sudo vim /etc/zabbix/zabbix_server.conf
	INSERT

		#decomentar e alterar o valor da variável DBPassword= na linha: 131
		DBPassword=zabbix
	
	#salvar e sair do arquivo
	ESC SHIFT : x <Enter>

	#editando o arquivo de configuração do Zabbix Agent
	sudo vim /etc/zabbix/zabbix_agentd.conf
	INSERT

		#deixar o padrão das variáveis Server= e ServerActive= nas linhas: 117 e 171
		Server=127.0.0.1
		ServerActive=127.0.0.1

		#alterar o valor da variável Hostname= na linha: 182
		Hostname=wsvaamonde
	
	#salvar e sair do arquivo
	ESC SHIFT : x <Enter>

#08_ Habilitando o Serviço do Zabbix Server e Agent<br>

	#habilitando o serviço do Zabbix Server e Agent
	sudo systemctl daemon-reload
	sudo systemctl enable zabbix-server zabbix-agent
	sudo systemctl restart zabbix-server zabbix-agent apache2

#09_ Verificando o Serviço e Versão do Zabbix Server e Agent<br>

	#verificando o serviço do Zabbix Server e Agent
	sudo systemctl status zabbix-server zabbix-agent
	sudo systemctl restart zabbix-server zabbix-agent
	sudo systemctl stop zabbix-server zabbix-agent
	sudo systemctl start zabbix-server zabbix-agent

	#verificando a versão do Zabbix Server e Agent
	#opção do comando zabbix_server: -V (version)
	#opção do comando zabbix_agentd: -V (version)
	sudo zabbix_server -V
	sudo zabbix_agentd -V

#10_ Configurando o Zabbix Server via Navegador<br>

	firefox ou google chrome: http://endereço_ipv4_ubuntuserver/zabbix

	#Configuração inicial do Zabbix Server
	Welcome to Zabbix 7.0
		Default language: English (en_US)
			<Next step>
		Check of pre-requisites
			<Next step>
		Configure DB connection
			Database type: MySQL
			Database host: localhost
			Database port: 0 (use default port)
			Database name: zabbix
			Store credentials in: Plain text
			User: zabbix
			Password: zabbix
			<Next step>
		Settings
			Zabbix server name: wsvaamonde
			Default time zone: (UTC-03:00) America/Sao_Paulo
			Default theme: Dark
			<Next step>
		Pre-installation summary
			<Next step>
		Install
			<Finish>

	#Acessando o Painel de Gerenciamento do Zabbix Server
	Username: Admin
	Password: zabbix
	Yes: Remember me for 30 days
	<Sign in>

#11_ Verificando a Porta de Conexão do Zabbix Server e Agent<br>

	#opção do comando lsof: -n (network number), -P (port number), -i (list IP Address), -s (alone directs)
	sudo lsof -nP -iTCP:'10050,10051' -sTCP:LISTEN

#12_ Adicionado o Usuário Local no Grupo Padrão do Zabbix Server<br>

	#opções do comando usermod: -a (append), -G (groups), $USER (environment variable)
	sudo usermod -a -G zabbix $USER
	newgrp zabbix
	id
	
	#recomendado reinicializar a máquina para aplicar as permissões
	sudo reboot

#13_ Localização dos diretórios principais do Zabbix Server e Agent<br>

	/etc/zabbix/*      <-- Diretório dos arquivos de Configuração do serviço do Zabbix
	/var/log/zabbix*   <-- Diretório dos arquivos de Log's do serviço do Zabbix
	/usr/share/zabbix* <-- Diretório dos arquivos do Site do serviço do Zabbix

#14_ Instalando os Agentes do Zabbix no Linux Mint e no Windows 10<br>

	#Link de referência do download: https://www.zabbix.com/br/download_agents

	Windows, Any, amd64, v6.4, No encryption, MSI: 6.4.12
	https://cdn.zabbix.com/zabbix/binaries/stable/6.4/6.4.12/zabbix_agent2_plugins-6.4.12-windows-amd64.msi

	#Instalação Manual do Zabbix Agent para Microsoft
	Pasta de Download
		Welcome to the Zabbix Agent (64-bit) Setup Wizard <Next>
		End-User License Agreement
			On I accept the therms in the License Agreement <Next>
		Custom Setup
			On Zabbix Agent <Next>
		Zabbix Agent service configuration
			Host name: windows10
			Zabbix server IP/DNS: 172.16.1.20
			Agent listen port: 10050
			Server or Proxy for active checks: 172.16.1.20
			Off Enable PSK
			On Add agent location to the PATH <Next>
		Ready to install Zabbix Agent (64-bit) <Install>
			Zabbix Agent MSI package (64)-bit <Sim>
		Completed the Zabbix Agent (64-bit) <Finish>
	
	#Verificação da instalação do Zabbix Agent no Powershell
	#opção do comando netstat: -a (All connections), -n (addresses and port numbers)
	Powershell
		hostname
		Get-Service Zabbix-Agent
		netstat -an | findstr 10050

	#Link de referência do download: https://www.zabbix.com/br/download
	
	7.0 PRE-RELEASE, Ubuntu, 22.04 (Jammy), Agent 2
	wget https://repo.zabbix.com/zabbix/6.5/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.5-1+ubuntu22.04_all.deb

	#instalando o repositório do Zabbix Agent2
	#opção do comando dpkg: -i (install)
	sudo dpkg -i zabbix-release_6.5-1+ubuntu22.04_all.deb

	#atualizando as lista do apt com o novo repositório do Zabbix Agent2
	sudo apt update

	#instalando as dependências do Zabbix Agent2
	sudo apt install traceroute nmap snmp snmpd snmp-mibs-downloader apt-transport-https \
	software-properties-common git vim

	#instalando o Zabbix Agent2
	#opção do comando apt: --install-recommends (Consider suggested packages as a dependency for installing)
	sudo apt install --install-recommends zabbix-agent2 zabbix-agent2-plugin-*

	#editando o arquivo de configuração do Zabbix Agent2
	sudo vim /etc/zabbix/zabbix_agentd.conf
	INSERT

		#alterar as linhas 117, 171 e 182:
		Server=172.16.1.20
		ServerActive=172.16.1.20
		Hostname=linuxmint213
	
	#salvar e sair do arquivo
	ESC SHFT : x <Enter>
	
	#habilitando o serviço do Zabbix Agent2
	systemctl enable zabbix-agent2
	systemctl restart zabbix-agent2

	#verificando o serviço do Zabbix Agent2
	sudo systemctl status zabbix-agent2

	#opção do comando lsof: -n (network number), -P (port number), -i (list IP Address), -s (alone directs)
	sudo lsof -nP -iTCP:'10050' -sTCP:LISTEN

#15_ Criando os Hosts de Monitoramento dos Agentes no Zabbix Server<br>

	#Criação dos Host GNU/Linux e Microsoft Windows no Zabbix Server
	Data collection
		Hosts
			<Create host>
				Host
					Host name: linuxmint213
					Visible name: linuxmint213
					Templates: <Select>
						Template group: <Select>
							Templates/Operating systems
							Linux by Zabbix agent <Select>
					Host groups: <select>
						Discovered hosts <Select>
					Interfaces: Add:
						Agent: 
							DNS name: 172.16.1.
							Connect to: DNS
							Port: 10050
					Description: Desktop Linux Mint 21.3
					Monitored by proxy: (no proxy)
					Enable: On
				<Add>
	
	Data collection
		Hosts
			<Create host>
				Host
					Host name: windows10
					Visible name: windows10
					Templates: <Select>
						Template group: <Select>
							Templates/Operating systems
							Windows by Zabbix agent <Select>
					Host groups: <select>
						Discovered hosts <Select>
					Interfaces: Add:
						Agent: 
							DNS name: 172.16.1.
							Connect to: DNS
							Port: 10050
					Description: Desktop Microsoft Windows 10
					Monitored by proxy: (no proxy)
					Enable: On
				<Add>

#15_ DESAFIO-01: 


=========================================================================================

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO ZABBIX SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do Zabbix realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/11-zabbix.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiozabbix 