---
title: Liberando acesso a m�quinas na nuvem Oracle.
date: 2017-05-11 00:18:23 Z
categories:
- posts
---


# Liberando acesso a m�quinas na nuvem Oracle.

Para liberar o acesso em m�quinas da nuvem Oracle, primeiro precisamos conhecer e entender 3 pontos base:
- Security  Applications
- Security lists 
- Security Rules.

Na aba Security Applications, temos acesso a configura��o de portas, por padr�o a Oracle j� nos ajuda deixando configurada as portas mais comuns tais como ssh, listener e rdp, mas tamb�m podemos configurar nossas pr�prias portas indo em **Network->Security Applications-> Create Security Application**, devemos dar um nome para essa porta, escolher qual tipo de protocolo vai tr�fegar por ela e por fim o range ou a porta a ser configurada.
Nesse ponto, ainda n�o estamos liberando nenhum acesso, s� estamos configurando as portas que v�o ser liberadas.

Imagine uma caixa onde todos os itens dentro dela(no nosso caso VMs) compartilham as mesmas regras e tem livre acesso , � para isso que serve uma **Security List**, todas as VMs que fa�am parte da mesma Security List herdam e compartilham as mesmas regras, uma m�quina pode participar de at� 5 Security Lists.
Essa imagem extraida do site da Oracle exemplifica muito bem isso:

http://docs.oracle.com/cloud/latest/stcomputecs/STCSG/img/GUID-377E5D0A-90D5-4B98-8681-7D8B418D65A4-default.gif

As Vms Inst_1, Inst_2 e Inst_3 est�o  "dentro" da Security List A que � parametrizada para n�o permitir conex�es externas a essas m�quinas, mas permitem que elas enviem comunica��o para fora da Security List, entre essas m�quinas, elas podem se comunicar pelo IP Privado em qualquer porta.

Uma Security Rule, � b�sicamente uma regra de firewall, j� configuramos as portas (Security Applications) e j� vimos como agrupar VMs para que elas tenham livre comunica��o e compartilhem regras, agora vamos realmente liberar o acesso a elas.


Indo em Network->Security Rules-> Create Security Rules, temos que entrar o nome da nossa regra(coloque um nome f�cil), defina se ela vai estar habilitada ou n�o, escolha a aplica��o que voc� deseja liberar(no nosso caso ssh) ou selecione all se vai liberar todas as portas(muito cuidado com isso!), em source, configure a origem da conex�o, no nosso caso vamos selecionar Security IP List e colocar public-internet e destino como uma Security List.

Com essa configura��o, todas as m�quinas que fa�am parte da Security list selecionada v�o ter o acesso liberado.


