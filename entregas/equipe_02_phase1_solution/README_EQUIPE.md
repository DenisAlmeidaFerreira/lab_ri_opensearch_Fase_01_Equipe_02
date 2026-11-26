# Equipe XX — Fase 1

Integrantes: [Denis Almeida Ferreira - 123210975], [Arlis Brito De Oliveira Filho]

ID: equipe_02

Configurações comparadas: veja `resultados_dev/comparison.csv`.

Configuração final: mode: "lexical", analyzer: "portuguese", bm25_k1: 0.9 e bm25_b: 0.75 (lexico_v4).

Justificativa: No conjunto data/dev, o lexico_v4 alcançou o melhor equilíbrio entre precisão no topo e cobertura, liderando em NDCG@10 (0.8532) e MRR@10 (0.8381) com Recall@100 em 0.9667. Como a base concentra a relevância no campo text (com title frequentemente vazio), apresenta forte variação entre respostas curtas/objetivas e documentos longos, além de variações lexicais e ruídos de formatação/codificação em trechos do corpus, o analyzer escolhido lidou melhor com as variações morfológicas e de grafia sem perder foco nos primeiros resultados como ocorreu com o standard (Recall@100 = 1.0, porém com queda relevante no topo). Ao mesmo tempo, reduzir bm25_k1 para 0.9 com bm25_b = 0.75 conteve o peso excessivo de repetições de termos e favoreceu a correspondência exata em consultas curtas frente a documentos mais extensos, elevando os itens mais relevantes para as primeiras posições.

justificatica 2: Escolhemos o lexico_v4 porque ele apresentou o melhor compromisso entre colocar a resposta certa no topo e manter uma boa cobertura no conjunto data/dev, registrando 0.8532 de NDCG@10, 0.8381 de MRR@10 e 0.9667 de Recall@100. Analisando os dados, notamos que a relevância fica concentrada no campo text (já que muitos títulos vêm vazios), num cenário que mistura respostas curtas, documentos extensos e ruídos de formatação. O analyzer adotado conseguiu normalizar bem essas variações lexicais sem sacrificar o ranqueamento inicial, superando o comportamento do standard — que até garantiu cobertura total (Recall@100 de 1.0), mas falhou em priorizar os melhores resultados no topo. Por fim, a calibragem do BM25 (k1 = 0.9 e b = 0.75) impediu que documentos longos ganhassem vantagem apenas por repetirem termos da consulta, favorecendo correspondências mais precisas para perguntas curtas.

Comando de reprodução, a partir da raiz do pacote: `python entregas/equipe_02_phase1_solution/run.py --data data/dev --out resultados/check_fase1 --index ri-equipe_XX-check-fase1`

Dificuldades conhecidas: [preencher ou informar nenhuma]
