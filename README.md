# GAN
Este repositório implementa uma rede gerativa adversária com base no conhecimento aprendido nos cursos da série GANs for good de deeplearning.ai no coursera com algumas modificações minhas.

A GAN, implementada a partir do curso, utiliza a função de perda de Wasserstein e o "discriminador" neste caso é chamado de crítico, porque em vez de retornar um valor entre 0 e 1, ele pode retornar qualquer valor real, correspondendo ao quão "real" ele avalia uma imagem, isso ajuda o gerador porque de outra forma o discriminador poderia melhorar rápido de mais, como sua tarefa é mais simples e produziria resultados muito próximos de 0 e 1, levando o gerador a parar seu treinamento (os gradientes ficariam infinitos, significando "não há como melhorar" e o gerador pararia de treinar)

Além do que aprendi no curso há também algumas modificações

A primeira modificação importante que eu fiz é que em vez de ter tamanhos de kernel e stride fixos as camadas nas funções make_gan_block e make_crit_block passam a ter o tamanho do kernel definido diretamente a partir das dimensões desejadas de entrada e saída. Isto é útil porque permite que a rede funcione independente da base de dados escolhida, antes se mudássemos a bases de dados teríamos que mudar os parâmetros internos ou o Gerador poderia gerar resultados que não fossem compatíveis com o crítico.

>>Para calcular o tamanho do kernel que mapearia as dimensões da entrada para a saída, me baseei na documentação do pytorch para as camadas de [Convolução](https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html#torch.nn.Conv2d) e [Convolução Transposta](https://pytorch.org/docs/stable/generated/torch.nn.ConvTranspose2d.html#torch.nn.ConvTranspose2d) para a partir das equações que indicam as dimensões de saída a partir de um dado kernel e stride concluir que dado um certo stride o tamanho do kernel que mapeia a entrada na saída deve ser:

> # para o gerador:
# K_h = H_out - stride*(H_in-1)
# K_w = W_out - stride*(W_in-1)
> # para o crítico:
# K_h = H_in - stride*(H_out-1)
# K_w = W_in - stride*(W_out-1)

# Onde:
>K_h e K_w são a altura e largura do kernel, respectivamente

>H_in e W_in são a altura e largura da entrada, respectivamente

>H_out e W_out são a altura e largura da entrada, respectivamente

Outra modificação importante que foi possível graças à primeira é que agora é possível especificar um número de camadas para cada rede, permitindo inclusive GANs de arquitetura profunda

As seguintes modificações a caminho:
> Tratar bases de dados externas ao pytorch de modo que os tipos sejam convertidos para não haver problemas de tipagem nos dados

> Dar continuidade aos conceitos aprendidos no curso, permitindo geração controlável e possivelmente geração condicional

>Fazer modificações que permitam a inserção segura de padding e o uso de strides diferentes nas redes de múltiplas camadas

> Embutir conhecimentos do próximo curso para tornar a GAN mais semelhante ao estado da arte
