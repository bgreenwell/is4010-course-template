# Lab 07: working with external data

## Objective

This lab is designed to give you hands-on practice with the two main ways applications interact with data: persisting it locally to files and fetching it from the web. You will build a simple contact book that saves its data to a JSON file and a separate script that consumes a live web API.

-----

## Prerequisites

For part 2 of this lab, you will need to install the `requests` library, which is the standard for making HTTP requests in python. Open your terminal and run the following command:
`pip install requests`

-----

## Part 1: the JSON contact book

### Your task

You will complete two functions to handle saving and loading a list of contacts using the JSON format.

1.  In your `is4010-labs` repository, create a new file named `lab07_contact_book.py`.
2.  Copy all the python code from the "contact book code" section below into this new file.
3.  Complete the `save_contacts_to_json` and `load_contacts_from_json` functions according to their docstrings. The `load` function must handle a `FileNotFoundError` gracefully.

### Contact book code

```python
import json

def save_contacts_to_json(contacts, filename):
    """
    Saves a list of contacts (dictionaries) to a file in JSON format.

    Parameters
    ----------
    contacts : list
        A list of contact dictionaries.
    filename : str
        The name of the file to save the contacts to.
    """
    # Use with open(...) and json.dump() to write the contacts list
    # to the specified file. Use an indent of 4 for readability.
    pass

def load_contacts_from_json(filename):
    """
    Loads a list of contacts from a JSON file.

    Parameters
    ----------
    filename : str
        The name of the file to load contacts from.

    Returns
    -------
    list
        A list of contact dictionaries. Returns an empty list if the
        file does not exist.
    """
    # Use a try...except block to handle the FileNotFoundError.
    # If the file exists, use with open(...) and json.load() to read
    # and return the contacts.
    # If the file does not exist, return an empty list.
    pass

if __name__ == '__main__':
    # Main execution block to test the functions
    contacts_file = 'contacts.json'

    # Try to load existing contacts
    my_contacts = load_contacts_from_json(contacts_file)
    print(f"Loaded {len(my_contacts)} contact(s).")

    # Add a new contact (as a dictionary)
    new_contact = {"name": "Charles Babbage", "email": "charles@computers.org"}
    my_contacts.append(new_contact)
    print(f"Added a new contact for {new_contact['name']}.")

    # Save the updated list of contacts
    save_contacts_to_json(my_contacts, contacts_file)
    print("Saved contacts to disk.")
```

-----

## Part 2: the API client

### Your task

For this part, you will write a script that fetches live data from a public web API and displays it.

1.  In your `is4010-labs` repository, create a new file named `lab07_api_client.py`.
2.  Choose a public API to work with. Here are some simple options that don't require an API key:
      * **Pokémon API**: `https://pokeapi.co/api/v2/pokemon/ditto`
      * **Open Trivia DB**: `https://opentdb.com/api.php?amount=1`
      * **Public APIs List**: `https://api.publicapis.org/random`
3.  Copy the python code from the "API client code" section below into your new file.
4.  Complete the `get_api_data` function. It should use the `requests` library to fetch data from the provided URL and return the parsed JSON. It must handle potential errors.

### API client code

```python
import requests

def get_api_data(url):
    """
    Fetches and parses JSON data from a given API url.

    Parameters
    ----------
    url : str
        The URL of the API endpoint.

    Returns
    -------
    dict or None
        A dictionary containing the parsed JSON data, or None if
        the request fails or the response is not valid JSON.
    """
    # Use a try...except block to handle potential requests.exceptions.RequestException
    try:
        # Make a GET request to the URL
        response = requests.get(url)
        
        # Raise an HTTPError if the response was an error
        response.raise_for_status()

        # Parse and return the JSON data
        return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Error making request: {e}")
        return None
    except requests.exceptions.JSONDecodeError:
        print("Error: Failed to decode JSON from response.")
        return None


if __name__ == '__main__':
    # Example using the Pokémon API
    pokemon_url = "https://pokeapi.co/api/v2/pokemon/snorlax"
    
    # Get the data from the API
    pokemon_data = get_api_data(pokemon_url)

    # If data was successfully fetched, display some of it
    if pokemon_data:
        print(f"Successfully fetched data for: {pokemon_data['name'].title()}")
        print(f"Weight: {pokemon_data['weight']} hectograms")
        print("Abilities:")
        for ability in pokemon_data['abilities']:
            print(f"  - {ability['ability']['name']}")

```

-----

## Submission

When you are finished, commit and push both `lab07_contact_book.py` and `lab07_api_client.py` to your `is4010-labs` github repository. The automated tests will check the functionality of your save and load functions from part 1.

```
git add lab07_contact_book.py lab07_api_client.py
git commit -m "Complete lab 07"
git push origin main
```