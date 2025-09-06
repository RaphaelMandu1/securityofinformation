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

<img width="1404" height="226" alt="image" src="https://github.com/user-attachments/assets/fae84499-0b25-4aba-91dd-58fcea340b8b" />




