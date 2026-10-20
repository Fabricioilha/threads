# Threads em ação

Uma página interativa em português para aprender o que são threads, por que são usadas, como funcionam e quais problemas trazem. O conteúdo parte da referência [arquitetura_de_sistemas_concorrentes.txt](./arquitetura_de_sistemas_concorrentes.txt) e está reunido em [index.html](./index.html).

**Criado por Fabricio Nascimento Siqueira.**

## Abrir a página

Não é necessário instalar dependências. A página é HTML, CSS e JavaScript sem bibliotecas externas.

No Windows, abra o PowerShell nesta pasta e execute:

```powershell
py -m http.server 8000
```

Depois, acesse [http://localhost:8000](http://localhost:8000) no navegador. Para encerrar o servidor, pressione `Ctrl+C` no terminal.

Também é possível abrir `index.html` diretamente no navegador. O servidor local é recomendado para uma experiência mais consistente.

## O que você vai aprender

- **Motivação:** diferenças entre processos e threads, custos de comunicação e o trade-off entre isolamento e memória compartilhada.
- **Ciclo de vida de um processo:** animação de novo, pronto, executando, esperando e encerrado, acompanhando CPU, memória virtual e informações didáticas do PCB.
- **Ciclo de vida:** criação, estado pronto, execução, bloqueio, retomada e término.
- **Escalonamento:** filas de tarefas, workers e núcleos de CPU, observando como tarefas concorrentes dividem os recursos.
- **Troca de contexto:** uma simulação passo a passo de uma thread bloqueada por I/O, com salvamento e restauração didáticos de PC, SP e registradores enquanto outra thread executa.
- **I/O e periféricos:** percurso da solicitação entre thread, CPU/runtime, kernel, controlador, dispositivo, conclusão e retomada; permite escolher dispositivo e latência ilustrativa, pausar e continuar.
- **Memória e hardware:** espaço virtual, pilhas, heap, caches, RAM, TLB, MMU, coerência de cache e false sharing.
- **Desafios de concorrência:** corrida de dados, deadlock, starvation, contenção e limites de pools.
- **Modelos de execução:** processos, threads nativas, pools, mapeamentos N:1, 1:1 e M:N, threads virtuais e event loops.
- **Glossário contextual:** passe o mouse ou mova o foco do teclado sobre siglas e termos técnicos sublinhados para ver sua explicação.

## Como usar as simulações

### Ciclo de vida e recursos

Na seção **Simulador**, cada bolinha `T` representa uma tarefa. As tarefas prontas aguardam um core; as bloqueadas aguardam o período de I/O; e as tarefas excedentes de um pool aguardam um worker.

Os parâmetros controlam:

- **Núcleos de CPU:** número máximo de tarefas que podem executar ao mesmo tempo.
- **Tarefas do cenário:** quantidade de trabalhos curtos que serão concluídos.
- **Chance de bloqueio por I/O:** probabilidade didática de uma tarefa parar para aguardar I/O durante seu trabalho.
- **Custo estimado por despacho:** valor usado para calcular o custo total de despachos; não é uma medição do computador.
- **Reserva de pilha nativa:** estimativa simplificada de memória associada a workers nativos.
- **Duração de espera de I/O:** número de ciclos didáticos em que uma tarefa permanece bloqueada.
- **Trabalho de CPU por tarefa:** unidades abstratas de cálculo; não representa MB nem simula cache.

A tabela **Resultados lado a lado** calcula automaticamente tempo em ciclos, vazão, despachos e memória estimada dos quatro modelos para o cenário atual. Selecione um modelo e pressione **Simular** para observar a animação. Os trabalhos e eventos de I/O são determinísticos, de modo que a animação corresponde aos resultados da tabela. Alterar qualquer parâmetro recalcula a comparação.

Para um experimento, configure 24 tarefas, 2 núcleos, 60% de chance de I/O e espera de 8 ciclos; observe a diferença entre **Thread**, **Thread Pool** e **Virtual Thread**. Depois reduza a chance de I/O a 0% e observe como o paralelismo continua limitado pelos núcleos.

Os ciclos, a vazão e a memória são saídas do modelo pedagógico, não medições reais. Os custos de criação, troca, isolamento, runtime, sistema operacional e dispositivo não são reproduzidos fielmente; processo, thread e virtual thread usam o mesmo escalonamento simplificado, enquanto o pool limita o número de workers.

### Ciclo de vida do processo

Na seção **Um processo em viagem pelo sistema operacional**, use **Anterior** e **Próxima etapa** para explorar as transições manualmente, ou **Reproduzir ciclo** para animar a sequência. É possível pausar e continuar ou reiniciar. A cena distingue o estado do processo, a thread que usa o core, o espaço virtual e os dados de controle do kernel. O exemplo representa um processo com uma única thread.

### Troca de contexto

Na seção **Dentro do core**, use **Anterior** e **Próximo** para estudar cada estado manualmente. **Reproduzir** avança a sequência automaticamente; o botão passa a permitir pausa e continuação. **Reiniciar** retorna ao início. Os registradores e endereços exibidos são exemplos didáticos, não valores lidos do computador.

### I/O com periféricos

Na seção **Quando a thread toca um periférico**, escolha um dispositivo e ajuste a latência ilustrativa. **Percorrer caminho** inicia a animação; durante a execução, o mesmo botão pausa ou continua na etapa atual.

## Notas sobre as estimativas

As animações e métricas são modelos pedagógicos simplificados, não benchmarks nem previsões de desempenho. O simulador usa ciclos artificiais e estimativas de memória; não mede a CPU, o sistema operacional, o runtime ou o dispositivo real. Latências e mecanismos efetivos variam conforme arquitetura, sistema e carga.

## Arquivos

- [index.html](./index.html) — página, estilos, conteúdo e lógica das simulações.
- [arquitetura_de_sistemas_concorrentes.txt](./arquitetura_de_sistemas_concorrentes.txt) — referência conceitual usada para o material.
