**Resumo.** O problema tratado no trabalho é  o “Problema dos Leitores e Escritores", caracterizado pelas threads, ou por dependência de dados para execução de processos. O problema dos Leitores e Escritores reproduz o acesso a uma base de dados, onde alguns processos estão tentando alterar a informação da região crítica, que são os escritores, e outros processos estão lendo os dados da região crítica, somente querendo obter a informação, que são os leitores.

**1. Introdução**

Este problema é uma abstração do acesso à base de dados, onde um grupo de tarefas acessa simultaneamente uma área de memória compartilhada onde podem ler ou escrever valores. Não há perigo de leituras simultâneas por vários processos, mas as gravações ou alterações nos dados devem ser feitas sob exclusão mútua para garantir a consistência e evitar condições de disputa.

**2. Leitores**

Processos, os quais não são requeridos excluir uns aos outros (entre eles) ou seja é um processo que pode ter vários leitores manuseando ao mesmo tempo a informação compartilhada visto que nenhum dos processos realizará mudanças na mesma.

**3. Escritores**

Um escritor é aquele que acessa a informação e faz alterações na mesma. Ou seja, são processos, os quais são requeridos para excluir todos os outros processos, que são os leitores e escritores. O acesso tende ser exclusivo para os escritores, já que o dado será alterado.

**4. Base de dados**

O conceito de banco de dados deve ser entendido em seu sentido mais amplo. Mesmo a tabela mais simples que descreve o status de uma unidade de disco ou um conjunto de janelas em uma tela de terminal pode ser vista como um exemplo de banco de dados que pode exigir algum tipo de solução para o problema de proteção de leitores e escritores.

**5. Threads**

Se implementadas corretamente, as threads têm vantagens sobre os processos, porque os fork() tem mais overhead do que as threads. Threads compartilham o mesmo espaço de endereçamento, economizando CPU. A comunicação entre threads é mais simples porque compartilham espaço de memória, enquanto fork() requer algumas técnicas como pipes.

Existe um padrão para criar e manipular threads chamado POSIX, e a biblioteca que implementa o POSIX é chamada Pthreads e é usada em sistemas como Linux, Solaris e Windows.
A necessidade de criar um padrão para o uso de threads é porque historicamente todo desenvolvedor de hardware implementou sua própria versão de threads, dificultando a portabilidade de programas usando threads.

Exemplo:
Em C é possível utilizar a biblioteca pthread.h que fornece funções que seguem o padrão POSIX. Para usar a biblioteca é necessário importar a biblioteca pthread.h que pode ser feito utilizando o trecho de código a seguir:

#include <pthread.h>

**6. Mutex**

A exclusão mútua é uma das principais formas de se implementar sincronização entre threads e proteger dados compartilhados durante a escrita. Sendo assim, apenas uma thread pode ter acesso a uma variável. São utilizados para prevenir condições de corrida.

Obs: Mutex também pode ser chamado de Variáveis de exclusão mútua.

**7. Semáforos**

Um semáforo é um mecanismo para resolver problemas de exclusão mútua. Um semáforo pode ser pensado como um objeto para o qual dois tipos de operações podem ser realizadas: bloquear e desbloquear a execução de instruções .
Os semáforos são implementados no sistema operacional e são considerados uma forma de IPC, os semáforos também podem ser usados ​​para sincronização e exclusão mútua.

**8. Solução**

Enquanto existir leitores na base de dados e um escritor estiver aguardando-o sair, logo que chegar um novo leitor, este é suspenso, em vez de ser admitido imediatamente.
Escritores precisam esperar que leitores ativos completem sua atividade.
Escritores não precisam esperar por leitores que chegam depois dele.

Observações:

A chegada de muitos leitores faz com que os escritores fiquem suspensos.
Se não parar de chegar leitores, os escritores nunca irão ter acesso a base de dados.
Escritores devem bloquear a base de dados quando estiverem escrevendo ela.

**9. Referências**

FAINA, Luís Fernando. Projeto de MC104 - SISTEMAS OPERACIONAIS Sincronização entre Processos: Mecanismo de Semáforos. UFU. 13 de setembro de 2006. Disponível em:<https://www.facom.ufu.br/~faina/MCC_Crs/MC104-2S2006/Prjt_SO/semaphor.html#:~:text=Sem%C3%A1foros%20s%C3%A3o%20mecanismos%20que%20resolvem,sobre%20um%20sem%C3%A1foro%20s%C3%A3o%20at%C3%B4micas>.

UEYAMA, Jó. Sistemas Operacionais. PowerPoint Presentation. Disponível em: <http://wiki.icmc.usp.br/images/7/76/Aula06.pdf>.

MAZIERO, Carlos. Sistemas Operacionais: Conceitos e Mecanismos, Problemas clássicos. UFPR. 2019. Disponível em: <http://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-12.pdf>.

Desconhecido. O PROBLEMA DOS LEITORES E ESCRITORES.  UFSC.  Disponível em: <http://www.inf.ufsc.br/~bosco.sobral/ensino/ine5645/Leitores-Escritores.pdf>.

MACEDO, Jorge Raul. Problema dos Leitores/Escritores. DOCPLAYER. 2018. Disponível em: <http://docplayer.com.br/68551323-Problema-dos-leitores-escritores.html#:~:text=5%20O%20problema%20de%20sincroniza%C3%A7%C3%A3o,uma%20mesma%20estrutura%20de%20dados>.

Venancius, Igor. C (pthreads). Programação Concorrente, 2019. Disponível em: <http://cocic.cm.utfpr.edu.br/progconcorrente/doku.php?id=c_pthreads>.
