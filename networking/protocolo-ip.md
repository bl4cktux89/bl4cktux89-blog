# Protocolo IP

> ⚠️ Disclaimer: o texto é baseado na RFC 791, no livro Redes de Computadores e as anotações que faço.

A ideia central é observar parte do contexto histórico e entender a sua importância, apresentar uma visão geral das funcionalidades e posteriormente mergulhar nos detalhes.

Agora sim, podemos começar e o faremos pelo início de tudo, lá na Guerra Fria, que ocorreu entre os Estados Unidos da América e a União das Repúblicas Socialistas Soviéticas, mas não vamos nos aprofundar no conflito, somente no que aconteceu a partir dele para o desenvolvimento das redes de computadores, como conhecemos atualmente.

A *ARPA* (*Advanced Research Projects Agency*, em português, Agência de Pesquisas em Projetos Avançados), tinha a necessidade de transmitir dados sigilosos entre as suas bases militares e departamentos de pesquisa, a partir dessa necessidade houve o surgimento da ARPAnet (*Advanced Research Projects Agency Network*, em português, Rede da Agência de Pesquisas em Projetos Avançados), que também incluía universidades e algumas empresas privadas, formando um grupo de trabalho chamado de *ARPANET Network Working Group*.

Muitos dos protocolos e tecnologias que utilizamos hoje em dia para nos comunicar têm sua origem na ARPAnet, que começou modesta, mas com o tempo, mais instituições se conectaram através de linhas telefônicas dedicadas.

Inicialmente o protocolo padrão para a internet era chamado de NCP (Network Control Program, Programa de Controle de Rede), mas com surgimento de redes de rádio e satélite, foram percebidos diversos desafios para os protocolos existentes, levando ao desenvolvimento de uma nova arquitetura chamada de modelo de referência TCP/IP que tem como ideias centrais:

- Permitir o roteamento entre redes diferentes
- Independência do hardware
- Recuperação de falhas

---

Mas afinal, do ponto de vista técnico, por que o protocolo IP foi desenvolvido?

A princípio, um dos principais problemas a serem resolvidos, era evitar o desperdício de recursos, antes da criação da comutação de pacotes, a comutação era realizada através de circuitos, que ao iniciar a comunicação entre uma origem e um destino, era criado um canal de comunicação dedicado e que consumia recursos da rede mesmo sem estar em uso, já na comutação por pacotes não é criado um canal de comunicação dedicado, os pacotes são transmitidos individualmente, sem uma rota pré-definida até o destino e possuem a vantagem de não ocupar o canal de comunicação em períodos de ociosidade.

> 💡 O protocolo IP foi projetado para o uso em sistemas baseados em comutação de pacotes e o seu escopo é atender as necessidades básicas para entregar dados partindo de uma origem em direção a um destino.

É importante observarmos que não existem quaisquer mecanismos para garantir a confiabilidade de dados, controle de fluxo, sequenciamento ou correção de erros, porém essas responsabilidades, são delegadas para os vizinhos presentes nas camadas de transporte e de enlace de dados.

O exemplo abaixo demonstra de forma simplificada a relação entre o protocolo IP e os protocolos das camadas adjacentes, imagine que um módulo TCP utilize o módulo de internet para enviar um segmento TCP (incluindo o cabeçalho TCP e os dados do usuário) como parte do pacote de internet:

1. O módulo TCP forneceria os endereços e outros parâmetros no cabeçalho de internet como argumentos para o módulo de internet (Camada de Transporte).
2. O módulo de internet então criaria o pacote de internet e chamaria a interface de rede local para transmiti-lo (Camada de Enlace).

> 💡 O protocolo IP implementa duas funções básicas: endereçamento e fragmentação.

- Endereçamento: os endereços IPv4 possuem 32 bits, separados em 4 octetos e não utiliza o sistema de classes de endereçamento desde a década de 90, por esse motivo a única importância é apenas o conhecimento histórico.
- Fragmentação: os pacotes são divididos em fragmentos, quando necessário, para serem transmitidos através de uma rede.

Os cabeçalhos possuem informações para transmitir pacotes aos respectivos destinos e a seleção de um caminho para realizar a transmissão é chamado de roteamento.

O Protocolo IP, utiliza campos no cabeçalho da internet para fragmentar e reagrupar datagramas quando necessário para a transmissão e os datagramas são vistos como entidades únicas, sem conexões ou circuitos lógicos.

O protocolo IP opera em cada host e *gateway* para interpretar campos de endereço, fragmentar e montar datagramas, tomar decisões de roteamento e outras funções.

O IP usa quatro mecanismos principais para desempenhar a sua função:

1. **Tipo de Serviço:** É um conjunto de parâmetros que define a qualidade do serviço desejado na rede. Isso ajuda os gateways a escolher os parâmetros de transmissão ideais ao rotear um pacote na Internet.
2. **Tempo de Vida:** Indica o limite máximo de vida útil de um pacote na Internet. Se esse limite for atingido (chegar a zero), o pacote é descartado. Funciona como uma "autodestruição" do pacote após certo tempo.
3. **Opções:** Oferecem funções de controle adicionais para situações específicas, como carimbos de tempo, segurança e roteamento especial. Geralmente não são usadas em comunicações cotidianas.
4. **Checksum do Cabeçalho:** Serve para proteger os campos do cabeçalho da internet contra erros de transmissão. Se o checksum falha, o pacote é descartado. Erros são relatados por meio do Protocolo ICMP (Internet Control Message Protocol).

> 💡 Gateway: em resumo, a função de um gateway é realizar a comunicação entre redes diferentes, sejam essas redes internas ou externas.