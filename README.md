# US51 - Aplicabilidade da teoria dos jogos em sistemas de recomendação
Dezembro de 2021

## VISÃO

Uma análise sobre a aplicabilidade da teoria dos jogos, mais especificamente o campo de estudos do pareamento de agentes de acordo com suas preferências.

## OBJETIVOS

* Determinar grupos de consumidores, lojistas, influenciadores
* Estudar as preferências dos diferentes grupos de modo a formar recomendações mais apuradas

## ESPECIFICAÇÕES

Após a realização da pesquisa bibliográfica preliminar para os estudos relativos ao desenvolvimento e implementação de um sistema de recomendações, observamos que os maiores desafios residem em gerar recomendações que atraiam os indivíduos para os quais aquelas são produzidas.

Estudos não relacionados diretamente com sistemas de recomendação abordam o agrupamento de agentes de acordo com suas preferências com aplicações em diversos campos tais como economia, propaganda e comportamentais com o objetivo de classificação dos agentes de modo a melhor enquadrá-los em categorias como ítens de consumo, atenção, objetivos pessoais ou sociais, etc.

Acreditamos que estes estudos apresentam potencialmente intersecção com o problema de gerar recomendações, facilitando a identificação de preferências de modo a melhorar a atratividade do que é recomendado para o indivíduo alvo.

## AGRUPAMENTO DE AGENTES EM UM SISTEMA DE RECOMENDAÇÕES

Um sistema de recomendações visa, de modo geral, recomendar ítens para consumidores. Com base em nosso estudo realizado em Outubro último (US#43, Sprint#4), abordamos as duas principais técnicas aplicadas na geração de recomendações:

* _Content-based_ - onde dados dos ítens são utilizados com heurísticas de agrupamento, com a vantagem de ser computacionalmente eficiente porém a desvantagem da baixa qualidade da recomendação gerada;
* _Collaborative-filtering_ - onde dados históricos e obsrvação de tendências são utilizadas para gerar recomendações, computacionalmente ineficiente e difícil de implementar quando não se possui o histórico necessário porém com a vantagem de resultar em recomendações de maior qualidade.

Podemos entender o sistema de recomendações como um jogo cooperativo, onde os participantes podem se comunicar livremente, porém a característica de pareamento é implícita (observamos a formação de grupos por interesses e afinidades comuns, como amantes de futebol ou por determinados times de futebol, amantes de churrasco, apreciadores de arte, entusiastas pela natureza, colecionadores de selos, etc.). Alguns destes grupos são bastante óbvios e especializados (como os citados), porém a maioria é bastante sutil, como por exemplo, pessoas interessadas em adquirir um eletro-portátil, ou em frequentar uma academia, ou ainda assistir uma determinada peça de teatro.

Compreendemos ainda o sistema de recomendações como um jogo de pareamento onde temos um número finito de influenciadores (os que recomendam ou endossam recomendações) e um número também finito de consumidores. Cada influenciador está disposto a recomendar alguns ítens, enquanto que os ouvintes estão dispostos a ouvir um número limitado de ofertas de diversos influenciadores até o limite de sua atenção. Recomendores e ouvintes são heterogêneos mas podemos arbtrariamente considerar a recomendação em si homogêneas. Cada agente (influenciador ou consumidor) derivam utilidade da atenção obtida ou dada com funções de utilidade aditivas. Em resumo, é um modelo muito-para-muitos de dois lados, com vetores de atenção, um para cada recomendação, e uma alocação de recomendação para ouvintes de modo que a demanda de cada um é satisfeita, o número de recomendações feitas pelo influenciador não é maior que a atenção disponível.

E finalmente, enquadramos o sistema de recomendações como um jogo cíclico, onde os jogadores (em nosso caso o influenciador e o consumidor) interagem repetidas vezes e baseaiam seu ganho nas iterações passadas. A função utilitária de cada agente está atenção dada pelo consumidor à recomendação, e recebida pelo influenciador. O consumidor ganha (e dá atenção) com boas recomendações, do mesmo modo que o influenciador (que ganha fazendo boas recomendações para quem está disposto a considerá-las). O pareamento perfeito entre influenciadores com reputação em determinado ítem e consumidores interessados no mesmo ítem garante o aproveitamento máximo da recomendação.

A Teoria dos Jogos tem um importante papel em sistemas de inteligência artificial, como por exemplo os que aplicam aprendizado por reforço,

Neste trabalho propomos utilizar a técnica de Agrupamento de Agentes da Teoria dos Jogos com diversos objetivos:

* Otimizar as heurísticas de agrupamento da abordagem Content-based de modo a melhorar a qualidade das recomendações produzidas; ou
* Otimizar a eficiência computacional da abordagem Collaborative-filtering classificando os agentes em seus grupos.

Outras possibilidades resultantes deste estudo são:

* Pareamento de agentes para maior efetividade da recomendação, i.e., parear de forma ótima influenciadores e recomendados e não só ítens para recomendados;
* Pareamento de agentes para maior efetividade do recomendado, i.e., parear de forma ótima itens recomendados por influenciadores, de forma a explorar o prestígio de quem recomenda determinado ítem.

### ALGORITMO DE GALE-SHAPLEY

1. Assinalar para cada consumidor _k_ que existem em _K_ e provedor _p_ que existem em _P_ como não pareado;
1. Pegar um _k_ não pareado, e que _p_ esteja no topo da lista de preferências de _k_:
    1. Se _p_ não estiver pareado, registrar _M(k) = P_;
    1. Se _p_ estiver pareado:
    1. Se _p_ prefere _k_ a _M-1(k)_ então registrar _M(k) = p_;
    1. Senão _k_ permanece não pareado e remove _p_ da lista de preferências.
1. Repetir 2 até que todo _k_ tenha sido pareado.

É fácil observar que este algorítmo é _O(n . m)_.

Uma demonstração do algoritmo pode ser observada vista em https://gitlab.com/stamps-group/gale-shapley/-/blob/master/simul.ipynb.

## PROBLEMAS DESTA ABORDAGEM

Podemos adiantar que esta abordagem não atende de forma realística o problema que nos propomos a resolver, pois as escolhas de pareamento de influenciadores por comerciantes e de produtos para influenciadores são relações _n x 1_, enquanto que a abordagem proposta ainda é _1 x 1_.

E ainda nesta linha de raciocínio, o problema se estende para relações _n x m_, onde por exemplo, tanto comerciantes quanto produtos podem ser atendidos por diversos influenciadores, ou o mesmo influenciador pode atender diversos comerciantes e produtos.

Estes são problemas que deverão ser endereçados em desenvolvimentos futuros.

## REFERÊNCIAS

1. Gale, David, and Lloyd S. Shapley. "College admissions and the stability of marriage." The American Mathematical Monthly 69.1 (1962): 9-15.