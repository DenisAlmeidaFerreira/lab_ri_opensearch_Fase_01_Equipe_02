# Equipe XX — Fase 1

Integrantes: [Denis Almeida Ferreira - 123210975]

ID: equipe_02

Configurações comparadas: veja `resultados_dev/comparison.csv`.

Configuração final: mode: "lexical", analyzer: "portuguese", bm25_k1: 0.9 e bm25_b: 0.75 (lexico_v4).

Justificativa: No conjunto data/dev, o lexico_v4 alcançou o melhor equilíbrio entre precisão no topo e cobertura, liderando em NDCG@10 (0.8532) e MRR@10 (0.8381) com Recall@100 em 0.9667. Como a base concentra a relevância no campo text (com title frequentemente vazio), apresenta forte variação entre respostas curtas/objetivas e documentos longos, além de variações lexicais e ruídos de formatação/codificação em trechos do corpus, o analyzer escolhido lidou melhor com as variações morfológicas e de grafia sem perder foco nos primeiros resultados como ocorreu com o standard (Recall@100 = 1.0, porém com queda relevante no topo). Ao mesmo tempo, reduzir bm25_k1 para 0.9 com bm25_b = 0.75 conteve o peso excessivo de repetições de termos e favoreceu a correspondência exata em consultas curtas frente a documentos mais extensos, elevando os itens mais relevantes para as primeiras posições.

Comando de reprodução, a partir da raiz do pacote: `python entregas/equipe_02_phase1_solution/run.py --data data/dev --out resultados/check_fase1 --index ri-equipe_XX-check-fase1`

Dificuldades conhecidas: [preencher ou informar nenhuma]
