# securityofinformation
securityofinformation

**Estou estudando na plataforma LETSDEFEND TRILHA DE SOC**
**ESSA MATERIA É DE BRUTEFORCE**

**Ferramentas usadas em ataques de força bruta**
Aircrack-ng : aircrack-ng é um programa de cracking de WEP/WPA 802.11a/b/g que pode recuperar uma chave WEP de 40, 104, 256 ou 512 bits após a coleta de pacotes criptografados suficientes. Também pode atacar redes WPA1/2 com alguns métodos avançados ou simplesmente por força bruta.

John the Ripper : John the Ripper é uma ferramenta projetada para ajudar administradores de sistemas a encontrar senhas fracas (fáceis de adivinhar ou quebrar por força bruta) e até mesmo enviar alertas automáticos aos usuários por e-mail, se desejado. Funciona em 15 plataformas diferentes, incluindo Unix, Windows e OpenVMS. 

L0phtCrack : uma ferramenta para quebrar senhas do Windows. Ela utiliza tabelas rainbow, dicionários e algoritmos multiprocessadores.

Hashcat : O Hashcat suporta cinco modos exclusivos de ataque para mais de 300 algoritmos de hash altamente otimizados. O hashcat atualmente suporta CPUs, GPUs e outros aceleradores de hardware no Linux e tem recursos para ajudar a distribuir quebras de senhas.

Ncrack : uma ferramenta para quebrar a autenticação de rede. Pode ser usada em Windows, Linux e BSD. Foi criada para ajudar empresas a proteger suas redes, testando proativamente todos os seus hosts e dispositivos de rede em busca de senhas fracas.

Hydra : Hydra é um cracker de login paralelizado que suporta diversos protocolos de ataque. É muito rápido e flexível, e novos módulos são fáceis de adicionar.

**Referência: kali.org/tools/**

**Como evitar ataques de força bruta?**

Para proteger sua organização de ataques de força bruta, imponha o uso de senhas fortes. 

Você pode encontrar algumas práticas recomendadas para senhas abaixo:

Nunca use informações que podem ser encontradas online (como nomes de familiares).
Tenha o máximo de caracteres possível.
Combine letras, números e símbolos.
Mínimo de 8 caracteres.
Cada conta de usuário é diferente.
Evite padrões comuns.

Política de bloqueio - Após um certo número de tentativas de login com falha, você pode bloquear contas e depois desbloqueá-las como administrador.

<img width="1138" height="565" alt="image" src="https://github.com/user-attachments/assets/9c748ad8-cbd6-437e-a51b-c551dfbe912c" />


Atrasos progressivos - Você pode bloquear contas por um tempo limitado após um certo número de tentativas de login com falha. 
Recaptcha - Com ferramentas como Captcha-reCAPTCHA, você pode tornar obrigatório que os usuários concluam tarefas simples para fazer login em um sistema. 

Política de senha forte - Você pode forçar os usuários a definir senhas longas e complexas e forçá-los a alterá-las periodicamente.

2FA - É o método onde uma segunda verificação é exigida do usuário com um mecanismo de verificação adicional (SMS, e-mail, token, notificação push, etc.) após inserir o nome de usuário e a senha.

Detecção de Ataques de Força Bruta
Regras específicas são geralmente definidas em sistemas SIEM para detectar ataques de força bruta. Ao definir essas regras, consideramos quantas tentativas de login malsucedidas são feitas pelo usuário em um determinado período. Durante a análise dos alarmes relevantes, os logs do protocolo/aplicativo de teste são examinados e as inferências necessárias são feitas. Exemplos de alguns ataques de força bruta são apresentados abaixo.

**Exemplo de detecção de ataque de força bruta SSH**
Senhas simples usadas no servidor com um ataque de força bruta SSH podem ser facilmente encontradas pelos invasores. Se tais ataques falharem, o invasor tentará apenas um certo número de senhas incorretas. Se for bem-sucedido, a senha será inserida com sucesso após um certo número de tentativas de login sem sucesso.

Em um exemplo de análise de força bruta SSH, quando visualizamos um log de máquina Linux com o conteúdo do arquivo “/var/log/auth.log.1” e tentativas de login com falha, podemos ver a quem pertencem as tentativas de login com falha.

cat auth.log.1 | grep "Falha na senha" | cut -d " " -f10 | sort | uniq -c | sort

<img width="1384" height="256" alt="image" src="https://github.com/user-attachments/assets/3c457432-80be-4084-b858-6da6a450a2d3" />

**Um comando como o abaixo pode ser usado para localizar os endereços IP que fizeram essas tentativas.**

cat auth.log.1 | grep "Falha na senha" | cut -d " " -f12 | sort | uniq -c | sort

<img width="1410" height="231" alt="image" src="https://github.com/user-attachments/assets/9cce3157-3a06-4f53-87f6-f61e01477183" />

Usuários que efetuarem login com sucesso também podem ser detectados com o seguinte comando.

cat auth.log.1 | grep "Senha aceita"

<img width="1281" height="312" alt="image" src="https://github.com/user-attachments/assets/00d03f0f-9ca2-40fc-bd37-4d96f6c204c6" />

Como pode ser visto aqui, tentativas de login bem-sucedidas são vistas com dois usuários diferentes de dois endereços IP diferentes.

Ao comparar as tentativas de login anteriores com falha, verifica-se que o usuário "analista" não havia realizado nenhuma tentativa de login malsucedida anteriormente com o endereço IP em que se conectou com sucesso. No entanto, observa-se claramente que muitas tentativas malsucedidas foram feitas com o usuário "letsdefend" no endereço IP 188.58.65.203. Isso nos mostra que o invasor se conectou com sucesso com o usuário "letsdefend" durante o ataque de força bruta.

<img width="1367" height="448" alt="image" src="https://github.com/user-attachments/assets/a9acb607-1736-4ee1-bdd1-c7db26bd1b3e" />

Como visto acima, usuários logados com e sem sucesso podem ser facilmente encontrados com comandos básicos do Linux. Quando esses dois resultados são examinados em detalhes, percebe-se que há uma entrada bem-sucedida após muitas tentativas malsucedidas do usuário letsdefend a partir do endereço IP 188.58.65.203.


**Registros de login do Windows**


Considerando a situação geral, uma atividade de login aparece em todos os ataques cibernéticos, bem ou malsucedidos. Um invasor frequentemente deseja efetuar login no servidor para assumir o controle do sistema. Para isso, pode realizar um ataque de força bruta ou efetuar login diretamente com a senha em mãos. Em ambos os casos (login bem-sucedido / tentativa de login malsucedida), o log será criado.

Considere um invasor conectado ao servidor após um ataque de força bruta. Para analisar melhor o que o invasor fez após entrar no sistema, precisamos encontrar a data de login. Para isso, precisamos do "ID do Evento 4624 – Uma conta foi conectada com sucesso".

Cada log de eventos tem seu próprio valor de ID. Filtrar, analisar e pesquisar o título do log é mais difícil, por isso é fácil usar o valor de ID.

Você pode encontrar os detalhes sobre qual valor de ID de evento significa o quê no endereço URL abaixo.

https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx

Arquivo de log da lição:

Log_File.zip Pass=321 (https://files-ld.s3.us-east-2.amazonaws.com/Log_File.zip)

Para chegar ao resultado, abrimos o “Visualizador de Eventos” e selecionamos os logs de “Segurança”.

<img width="579" height="511" alt="image" src="https://github.com/user-attachments/assets/3e9c6519-084f-45d8-ba5b-cffb592dac66" />

Em seguida, criamos um filtro para o ID do evento “4624”.

<img width="1341" height="759" alt="image" src="https://github.com/user-attachments/assets/75b35a1f-d892-44e4-b03e-9f6306a18662" />

Agora, vemos que o número de logs diminuiu significativamente e estamos listando apenas os logs de logins bem-sucedidos. Observando os detalhes do log, vemos que o usuário "LetsDefendTest" fez login pela primeira vez em 23/02/2021, às 22h17.

<img width="1129" height="795" alt="image" src="https://github.com/user-attachments/assets/22c238f4-a7f9-4f18-bed8-ef7cded447fe" />

Quando olhamos para o campo “Tipo de Logon”, vemos o valor 10. Isso indica que você está logado com “Serviços de Área de Trabalho Remota” ou “Protocolo de Área de Trabalho Remota”.

Você pode encontrar o significado dos valores do tipo de logon na página da Microsoft.

https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624

Na próxima seção, detectaremos o ataque de força bruta que o invasor fez antes de efetuar login.

**Detecção de força bruta do Windows RDP**

Nesta seção, capturaremos um invasor que está na fase de movimento lateral. O invasor está tentando saltar para a outra máquina por força bruta via RDP.

Baixar arquivo de log: Log_File.zip Pass=321

Log_File.zip Pass=321 (https://files-ld.s3.us-east-2.amazonaws.com/Log_File.zip)

Quando uma operação de login malsucedida é realizada no RDP, o log "ID do Evento 4625 - Falha ao efetuar login em uma conta" é gerado. Se seguirmos esse log, podemos rastrear o invasor.

<img width="1400" height="785" alt="image" src="https://github.com/user-attachments/assets/1b17f14b-3f78-4da8-a64c-7fdc099b27bc" />

Após a filtragem, vemos 4 logs com 4625 IDs de eventos.

<img width="1124" height="282" alt="image" src="https://github.com/user-attachments/assets/3b876a85-6bb2-4c9d-86f1-b18a0352c54b" />

Ao analisarmos as datas, vemos que os logs são gerados um após o outro. Ao analisarmos os detalhes, vemos que todos os logs são criados para o usuário "LetsDefendTest".

<img width="1270" height="665" alt="image" src="https://github.com/user-attachments/assets/84f6434a-48d6-4044-b7f5-120095f59d48" />

Como resultado, entendemos que o invasor tentou fazer login sem sucesso 4 vezes. Para entender se o ataque foi bem-sucedido ou não, podemos pesquisar os 4624 logs que vimos na seção anterior.

<img width="840" height="801" alt="image" src="https://github.com/user-attachments/assets/2902d3b2-7bc4-4c7a-b269-d1f125b9d0fb" />

<img width="1123" height="639" alt="image" src="https://github.com/user-attachments/assets/b641c9c3-4cea-4567-a4d6-377f2fac9d8b" />

Como pode ser visto nos resultados, o invasor conseguiu se conectar ao sistema com o log 4624 após os logs 4625.

<img width="682" height="434" alt="image" src="https://github.com/user-attachments/assets/be50fa7f-812d-4d12-972d-c75405d0d956" />













