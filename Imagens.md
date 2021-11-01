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
```python
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
```

### Calculo do Preto e Branco de uma imagem:

O codigo a baixo está escrito em _python_.
```python
from PIL import Image
from PIL import ImageEnhance

image = Image.open("images/newYork.jpg")
img_data = image.getdata()

lst = []
for i in img_data:
	lst.append(i[0]*0.2125 + i[1]*0.7174 + i[2]*0.0721)

new_img = Image.new("L", image.size)
new_img.putdata(lst)

new_img.save("black_white.jpg")
```

### Calculo da inversão da imagem:

O codigo a baixo esta escrito em _python_.
```python
# Load image
input_image = Image.open("images/newYork.jpg")
input_pixels = input_image.load()

# Create output image
output_image = Image.new("RGB", input_image.size)
draw = ImageDraw.Draw(output_image)

# Copy pixels
for x in range(output_image.width):
	for y in range(output_image.height):
		xp = input_image.width - x - 1
		draw.point((x, y), input_pixels[xp, y])

output_image.save("flip.jpg")
```

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

### Obter os canais de cor de uma imagem:
O código a baixo abaixo sepera os canais de cor de uma imagem. Esta escrito em _python_.
```python
from PIL import Image
import numpy as np

img = Image.open('image.png').convert('RGB')

def channel(img, n):
	""" n = 0: red, 1: green, 2: blue """
	a = np.array(img)
	a[:,:,(n != 0, n != 1, n != 2)] *= 0
	return Image.fromarray(a)

# RED IMAGE
red = channel(img, 0)
red.save("red.png")

# GREEN IMAGE
green = channel(img, 1)
green.save("green.png")

# BLUE IMAGE
blue = channel(img, 2)
blue.save("blue.png")
```

<p>O resultado final é o seguinte sem o preto e branco:

![](https://waltermattos.com/site/wp-content/uploads/2017/08/Poder_Curvas_Photoshop_Canais_RGB_Mistura.jpg)

### Modelo CMYK:
- Próprio para os **objetos que refletem luz**;
- Para obter as matrizes desejadas procede-se à **subtração das cores refeltida por uma superfício branca**;
- Seja uma fonte luminosa branca emitindo em direções de três filtros cião, magenta e amarelo:
	- **Ciano** (verde, azul): opôes-se à passagem do vermelho;
	- **Magenta**(vermelho, azul): opõe-se à passagem do verde;
	- **Amarelo**(verde, vermelho): opõe-se à passagem da cor azul.
	- 
### Formatos de ficheiros mais comuns:
	RGB:
	- jpg
	- png
	- gif
	- psd

<p>

	CMYK:
	- AI
	- PDF
	- EPS

### Modelo HSV:

- __H (Hue)__ -> Representa o tom.
- __S (Saturation)__ -> saturação da cor. Quanto mais baixo for a saturação, mais cizento é a cor. Quando a saturação é zero a cor é cizento.
- __V (Values)__ -> Representa a intensidade luminosidade. O brilho é determinado pelo grau de refletividade da superfície física que recebe a luz. Quanto maior for o brilho mais clara é a cor.

![](https://miro.medium.com/max/1400/0*YOMaPWRcXqAdKBbl.)

## Imagens Bitmap:
### Tamnho e Resolução:

	Profundidade -> número de bits para codificar um pixel.

<p>

	Podemos dividir as imagens bitmap em várias categorias:
	- imagens em dois níveis (preto e branco), com 1 bpp;
	- imagens em níveis de cizento, com 8 bpp;
	- imagens em cor indexada, com 8 bpp;
	- imagens "true color", com 24 bpp (+ componente alpha)
