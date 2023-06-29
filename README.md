# itogovaya
import requests

proxies = {
  "http": "http://localhost:8866",
  "https": "http://localhost:8866",
}

def get_pokemon_info(name):
    try:
        response = requests.get(f'https://pokeapi.co/api/v2/pokemon/{name}', verify=False)
        response.raise_for_status()

        pokemon_info = response.json()
        print(f'Покемон: {name}')
        print(f'Опыт: {pokemon_info["base_experience"]}')
        print(f'Вес: {pokemon_info["weight"]}')
        print(f'Типы: {[type_info["type"]["name"] for type_info in pokemon_info["types"]]}')

        return pokemon_info

    except requests.exceptions.HTTPError as err:
        print(f'Ошибка: {err}')
        return None


name = input('Введите имя покемона: ')
get_pokemon_info(name)
