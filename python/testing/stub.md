### 2. Stubs in Testing (Test Doubles)

In software testing, a stub is a type of "test double"—a fake object that replaces a real dependency. A stub's job is to provide pre-defined, "canned" answers to calls made during a test. It doesn't have any logic of its own.

**Key Purpose:** To isolate the code you are testing from external dependencies like databases, APIs, or complex objects. This makes tests faster, more predictable, and prevents them from having side effects.

**Example using `unittest.mock`:**

Imagine you want to test this function without making a real network request.

```python
# data_service.py
import requests

def get_username(user_id):
    """Fetches a username from a remote API."""
    response = requests.get(f"https://api.example.com/users/{user_id}")
    response.raise_for_status()
    return response.json()["username"]

# test_data_service.py
import unittest
from unittest.mock import patch, Mock
import data_service

class TestDataService(unittest.TestCase):
    @patch("data_service.requests.get")
    def test_get_username_returns_correct_name(self, mock_get):
        # 1. Configure the stub to return a fake response
        fake_response = Mock()
        fake_response.json.return_value = {"username": "testuser"}
        mock_get.return_value = fake_response

        # 2. Call the function
        username = data_service.get_username(1)

        # 3. Assert the result
        self.assertEqual(username, "testuser")
        mock_get.assert_called_once_with("https://api.example.com/users/1")