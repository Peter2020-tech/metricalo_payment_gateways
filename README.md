Payment Processing System

A flexible payment processing system built using PHP 8 and Symfony 6.4. It supports processing payments via two external payment processors: Shift4 and ACI, both through an API and a CLI command.
Features

    API endpoint for payment processing.
    CLI command for payment processing.
    Supports two payment processors: Shift4 and ACI.
    Unified response format for consistency.
    Extensible to add more processors in the future.

Requirements

    PHP 8.0 or higher
    Symfony 6.4
    Composer
    XAMPP (or any other web server environment)

Installation

    Clone the repository:

    bash

git clone https://github.com/yourusername/payment-system.git
cd payment-system

Install dependencies: Run the following command to install all required packages:

bash

composer install

Configure the environment: Create a .env.local file and configure your database and other necessary settings. For example:

makefile

DATABASE_URL="mysql://root:password@127.0.0.1:3306/paymentsystem"

Set up the database: Run the following commands to create the database and schema:

bash

php bin/console doctrine:database:create
php bin/console doctrine:schema:update --force

Run the Symfony server: To start the Symfony development server, run:

bash

    symfony server:start

    The application should now be accessible at http://localhost:8000.

API Usage
Endpoint

    URL: /app/example/{processor}
    Method: POST
    Processors: shift4 or aci

Input Parameters

The request should include the following parameters:
Key	Value Type	Description
amount	float	The amount to be charged
currency	string	The currency code (e.g., USD)
card_number	string	The credit card number
card_exp_year	int	The card expiry year
card_exp_month	int	The card expiry month
card_cvv	string	The CVV code of the card
Example Request (Postman)

json

{
  "amount": 100.00,
  "currency": "USD",
  "card_number": "4111111111111111",
  "card_exp_year": 2025,
  "card_exp_month": 12,
  "card_cvv": "123"
}

Response
Field	Description
transaction_id	The ID of the processed transaction
created_at	The date and time of the transaction
amount	The processed amount
currency	The currency used
card_bin	The first six digits of the card

Example response:

json

{
  "transaction_id": "shift4_txn_id",
  "created_at": "2024-10-01 12:00:00",
  "amount": "100.00",
  "currency": "USD",
  "card_bin": "411111"
}

CLI Usage

You can also process payments via the CLI:

bash

php bin/console app:example {processor} {amount} {currency} {card_number} {card_exp_year} {card_exp_month} {card_cvv}

Example:

bash

php bin/console app:example shift4 100.00 USD 4111111111111111 2025 12 123

Extending with More Processors

To add more payment processors, you can:

    Create a new class that implements PaymentProcessorInterface.
    Add the new class to PaymentService.
    Update the processPayment method to handle the new processor.

Testing

To run unit tests for the application, use the following command:

bash

php bin/phpunit  
