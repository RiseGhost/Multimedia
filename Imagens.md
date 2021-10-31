## Imagens Bitmap:
- Representam-se como matriz de pixéis;
- Não descrevem a imagem recorrendo a modelos matemáticos;
- As operações de edição normalmente pertimem criar e/ou modificar o aspeto dos pixéis que a constituem;<p>
![](https://wagnergaspar.com/wp-content/uploads/2021/05/3.png)
	
- O pixel é pois o elemento mais pequeno de resolução de uma imagem;
- O pixel aspect ratio é um valor numérico que representa a razão entre a largura do pixel e a sua altura;
- Os ___bitmaps___ igonaram a semântica (ou o significado) da informação que representa.

## Operações com imagens bitmap:
### Calculo do negativo da imagem:

O negativo de uma imagem é calculado subtraindo ao 255 o valor de vermelho ou verde ou azul.
O código abaixo se encontra escrito em _phyton_.
:::python hl_lines = "18 41"
~~~	
from PIL import Image

image = Image.open("images/newYork.jpg")

#create a new image
negative_image = Image.new(image.mode, image.size, 'white')
negative_save.save("negative.jpg")

#negative algorithm
for i in range(0, image.size[0] - 1):
	for j in range(0, image.size[1]-1):

		# Get pixel value at (x,y) position of the image
		pixelColorVals = image.getpixel((i,j))

		# Invert color
		redPixel = 255 - pixelColorVals[0] # Negate red pixel
		greenPixel = 255 - pixelColorVals[1] # Negate green pixel
		bluePixel = 255 - pixelColorVals[1] # Negate blue pixel

		# Modify the image with inverted pixel values
		negative_image.putpixel((i,j),(redPixel, greenPixel, bluesPixel))

negative_image.save("negative.jpg")
~~~

## Cor e codificação de cor:
### Conceitos Gerais:
- Luz: onde eletromagnética;
- Lus visível: entre os 400nm e os 700nm;
- Cor: comprimenton de onda da luz;
- Luz branca: todas as cores do arco iris;
- O olho humano sente o espectro de cores usando os cones e bastonentes.
### Modelo Aditivo e Subtractivo:
	Modelo aditivo:
	Descreve as cores emitidas ou projetadas, utilização em monitores.

![](https://i1.wp.com/www.hisour.com/wp-content/uploads/2018/03/RGB-color-model.jpg?w=720&ssl=1)

	Modelo Subtrativo:
	Descreve as cores impressas, utilização em impressoras.

![](https://i.loli.net/2019/07/05/5d1ec42acc42b55587.png)

### Modelo RGB:
- Três cores primárias: **vermelho**, **verde** e o **azul**;
- Ecrãs de vídeo (ex: computador, televisão) que restituem os tons pela adição das três cores primárias;
- Um tom é obtido através de uma combinação linear θ= ρ × R + γ × G + β × B, com (ρ, γ, β) ∈ [0, 1]^3;
- Considerando uma base de um byte para cada cor podemos modelar 2^8 x 2^8 x 2^8 = 2^24 = 1677716 cores;
- Uma imagem em modo 16 milhões de cores é conhecida por imagem em "true color".<p>

![](https://ramonpage.com/assets/images/posts/rgb-cube.png)

- **Origem**: ponto onde os três valores são iguas a 0 e que corresponde ao preto;
- **Vértice oposto**: ponto onde os valores das três coordenadas é máximo e por isso corresponde ao branco;
- **Vértice do cubo equistantes de duas cores primárias**: encontram-se as cores secundárias: amarelo, magenta e cião;
- Este modelo é **dependente dos periféricos** utilizados na aquisão e na representação.

![](http://4.bp.blogspot.com/-XSebXPhPo-Q/TV0BeHJUW7I/AAAAAAAAAAU/M5J9Sc7KH-0/s1600/sdabvksdlkf.jpg)

### Modelo CMYK:
- Próprio para os **objetos que refletem luz**;
- Para obter as matrizes desejadas procede-se à **subtração das cores refeltida por uma superfício branca**;
- Seja uma fonte luminosa branca emitindo em direções de três filtros cião, magenta e amarelo:
	- **Ciano** (verde, azul): opôes-se à passagem do vermelho;
	- **Magenta**(vermelho, azul): opõe-se à passagem do verde;
	- **Amarelo**(verde, vermelho): opõe-se à passagem da cor azul.
