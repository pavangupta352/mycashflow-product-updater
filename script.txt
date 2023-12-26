import requests
from requests.auth import HTTPBasicAuth


def update_product(store_name, product_id, auth_username, auth_password, update_data):
    """
    Updates a product in the MyCashflow system.

    Parameters:
    store_name (str): The name of the store.
    product_id (int): The unique identifier for the product.
    auth_username (str): The username for HTTP Basic Authentication.
    auth_password (str): The password for HTTP Basic Authentication.
    update_data (dict): The data to be updated.

    Returns:
    dict: The response from the server.
    """

    url = f"https://{store_name}.mycashflow.fi/api/v1/products/{product_id}"
    headers = {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }

    response = requests.patch(url, json=update_data, auth=HTTPBasicAuth(
        auth_username, auth_password), headers=headers)

    if response.status_code == 200:
        print("Product updated successfully.")
        return response.json()
    else:
        print(f"Failed to update product. Status code: {response.status_code}")
        return response.json()


store_name = "examplestore"
product_id = 123  # Replace with actual product ID
auth_username = "your_username"  # Replace with your username
auth_password = "your_password"  # Replace with your password

# Update data
update_data = {
    "name": "Updated Dress",
    "price": 169.99,
    # Add other fields you want to update
}

# Update the product
response = update_product(store_name, product_id,
                          auth_username, auth_password, update_data)
print(response)
