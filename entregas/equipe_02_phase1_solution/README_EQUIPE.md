# Equipe 02 — Fase 1

Integrantes: [Denis Almeida Ferreira - 123210975], [Arlis Brito De Oliveira Filho - 122210510], [Antonio Barros de Alcantara Neto - 123110363]

ID: equipe_02

Configurações comparadas: veja `resultados_dev/comparison.csv`.

Configuração final: mode: "lexical", analyzer: "portuguese", bm25_k1: 0.9 e bm25_b: 0.75 (lexico_v4).

Justificativa: Escolhemos o lexico_v4 porque, no conjunto data/dev, ele apresentou o melhor equilíbrio entre colocar a resposta certa no topo e manter uma boa cobertura, ficando à frente em NDCG@10 (0.8532) e MRR@10 (0.8381) com Recall@100 de 0.9667. Analisando os dados, notamos que a relevância fica concentrada no campo text, já que o campo title está vazio em todos os 10.000 documentos, num cenário que mistura respostas curtas, documentos extensos, variações lexicais e ruídos de formatação/codificação. O analyzer portuguese lidou melhor com essas variações morfológicas e de grafia sem sacrificar o ranqueamento inicial, superando o standard — que até garantiu cobertura total (Recall@100 = 1.0), mas falhou em deixar no topo os melhores resultados. Por fim, a calibragem do BM25 (k1 = 0.9 e b = 0.75) conteve o peso em excesso das repetições de termos, impedindo que documentos longos ganhassem vantagem apenas por repeti-los, e favoreceu correspondências mais precisas em consultas curtas, elevando os itens com maiores relevâncias para as primeiras posições.

Comando de reprodução, a partir da raiz do pacote: `python entregas/equipe_02_phase1_solution/run.py --data data/dev --out resultados/check_fase1 --index ri-equipe_02-check-fase1`

Dificuldades conhecidas: A maior dificuldade foi equilibrar cobertura e precisão no topo do ranking: o analyzer standard encontrou todos os documentos relevantes (Recall@100 = 1.0), mas os colocou em posições piores que o portuguese (NDCG@10 de 0.7649 contra 0.8532). A base também exigiu atenção: o campo title está vazio em todos os documentos, o tamanho dos textos varia muito e há ruídos como caracteres corrompidos e palavras sem espaço.
