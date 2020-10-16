# GAN
Este repositório implementa uma rede gerativa adversária com base no conhecimento aprendido nos cursos da série GANs for good de deeplearning.ai no coursera com algumas modificações minhas.

A GAN, implementada a partir do curso, utiliza a função de perda de Wasserstein e o "discriminador" neste caso é chamado de crítico, porque em vez de retornar um valor entre 0 e 1, ele pode retornar qualquer valor real, correspondendo ao quão "real" ele avalia uma imagem, isso ajuda o gerador porque de outra forma o discriminador poderia melhorar rápido de mais, como sua tarefa é mais simples e produziria resultados muito próximos de 0 e 1, levando o gerador a parar seu treinamento (os gradientes ficariam infinitos, significando "não há como melhorar" e o gerador pararia de treinar)

Eu inicialmente tinha definido uma forma de criar as camadas das redes automaticamente, inclusive definindo uma função matemática para o formato do kernel, porém essa metodologia impunha várias restrições levando o sistema a convergir de forma sub ótima; além do mais me dei conta que tal coisa não era necessária, pois caso se queira utilizar uma base de dados diferente basta mudar o tamanho das imagens; apesar disso, o que eu havia feito ainda poderia servir caso se queira utilizar redes de múltiplas camadas, no entanto seria necessário tratar melhor os demais hiperparâmetros para que a rede atinja um desempenho adequado e, portanto, tal coisa fica como uma possível modificação futura

As seguintes modificações a caminho:
> Tratar bases de dados externas ao pytorch de modo que os tipos sejam convertidos para não haver problemas de tipagem nos dados

> Dar continuidade aos conceitos aprendidos no curso, permitindo geração controlável e possivelmente geração condicional

> Embutir conhecimentos do próximo curso para tornar a GAN mais semelhante ao estado da arte

> Modificar o código para permitir uma forma eficiente e simplificada de criar GANs com redes de múltiplas camadas com tamanho definido pelo usuário
