from urllib.request import urlopen
from PIL import Image
import matplotlib.pyplot as plt
import requests

def obtener_info_pokemon(nombre):
    url = f"https://pokeapi.co/api/v2/pokemon/{nombre.lower()}"
    response = requests.get(url)

    if response.status_code == 200:
        pokemon_data = response.json()
        return pokemon_data
    else:
        return None
    
def mostrar_info_pokemon(data):
    if data:
        print(f"Nombre: {data['name'].capitalize()}")
        print("Habilidades:")
        for ability in data['abilities']:
            print(f"- {ability['ability']['name'].capitalize()}")
        print(f"Peso: {data['weight']}")
        print(f"Altura: {data['height']}")
        print("Tipos:")
        for poke_type in data['types']:
            print(f"- {poke_type['type']['name'].capitalize()}")
        print(f"Imagen frontal: {data['sprites']['front_default']}")
    else:
        print("¡Pokémon no encontrado!")

def main():
    nombre_pokemon = input("Ingresa el nombre del Pokémon: ")
    datos_pokemon = obtener_info_pokemon(nombre_pokemon)
    mostrar_info_pokemon(datos_pokemon)
 
api_url_pokemon = 'https://pokeapi.co/api/v2/pokemon/pikachu'
result = requests.get(api_url_pokemon)


if __name__ == "__main__":
    main()
    
if result.status_code == 200:
    pokemon_data = result.json()
    url_image = pokemon_data['sprites']['other']['official-artwork']['front_default']
    im = Image.open(urlopen(url_image))
    plt.imshow(im)
    plt.show()


