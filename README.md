# Multichain

Controle de ficha pessoal usando blockchain

Configure seu blockchain usando Multichain com Vagrant.
[Vagrant]: https://www.vagrantup.com/
[Multichain]: http://www.multichain.com/

* Acesse a pasta servidor e via terminal crie a máquina virtual do servidor e acesse usando os comandos abaixo:

        $ vagrant up
        $ vagrant ssh

* Acesse a pasta cliente e via terminal crie a máquina virtual do cliente e acesse usando os comandos abaixo:

        $ vagrant up
        $ vagrant ssh

* Dentro da VM do servidor, crie o blockchain:

        $ multichain-util create fichaPessoal

* Dentro da VM do servidor inicialize o blockchain:

        $ multichaind fichaPessoal -daemon

* Dentro da VM do cliente acesse o blockchain do servidor:

        $ multichaind fichaPessoal@10.4.4.4:4401 -daemon

* Dentro da VM do servidor, adicione as permissões de conexão:

        $ multichain-cli fichaPessoal grant 1F6km6qxta5p5gqtFF3XMCspKT1cCsDDeCADuS connect,send,receive

* Dentro do servidor do cliente, tente conectar novamente:

        $ multichaind fichaPessoal@10.4.4.4:4401 -daemon

* Acesse o modo interativo do blockchain fichaPessoal:

        $ multichain-cli fichaPessoal
        fichaPessoal: getinfo
        {
            "version" : "1.0 alpha 16",
            "protocolversion" : 10003,
            "chainname" : "fichaPessoal",
            "description" : "MultiChain fichaPessoal",
            "protocol" : "multichain",
            "port" : 4401,
            "setupblocks" : 60,
            "nodeaddress" : "fichaPessoal@192.1.2.46:4401",
            "burnaddress" : "1XXXXXXWsXXXXXXXRXXXXXXXZxXXXXXXat6JD4",
            "walletversion" : 60000,
            "balance" : 0.00000000,
            "blocks" : 55,
            "timeoffset" : 0,
            "connections" : 2,
            "proxy" : "",
            "difficulty" : 0.00001526,
            "testnet" : false,
            "keypoololdest" : 1457004398,
            "keypoolsize" : 2,
            "paytxfee" : 0.00000000,
            "relayfee" : 0.00000000,
            "errors" : ""
        }
# Criando e recuperando os dados no blockchain

Obs.: Todos os valores informados são em hexadecimal, exceto a chave da ficha, que nesse exemplo é o CPF, nossa chave de recuperação dos dados.

CPF de exemplo: 123456789-10

Cria um registro para o cpf informado:

        $ create stream 12345678910 true
        
Atribui um valor para o campo nome da ficha com o cpf informado:
        
        $ publish 12345678910 nome 416e646572736f6e204a6566666572736f6e20436572717565697261
        
Lista todos os registros de todas as pessoas que constam no blockchain:
        
        $ liststreams
        
Lista todos os itens do cpf informado:
        
        $ liststreamitems 12345678910
        
Cria um campo endereço com um valor para o cpf informado:
        
        $ publish 12345678910 endereco 505043412d554e42
        
Lista o campo nome do cpf informado:
        
        $ liststreamkeyitems 12345678910 nome
