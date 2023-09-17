# azure_flask_deployment

Deployed azure_flask_deployment url: https://eugene-504-flask.azurewebsites.net

## Set up and deploy the application steps: 

1. Create a new repository 'azure_flask_deployment ```azure_flask_deployment``` on GitHub and add a readme file.
2. Go to ```<> Code``` , copy link, go shell type: ```git clone <URL>```
3. Go file, open, find repository, click
4. Create a new file ```app.py```
```
from flask import Flask, render_template
import pandas as pd
import random
from faker import Faker

fake = Faker()

app = Flask(__name__)

@app.route('/')
def mainpage():
    return render_template('base.html')

@app.route('/about')
def aboutpage():
    return render_template('about.html')

@app.route('/random')
def randomnumber():
    number_var = random.randint(1, 10000)
    fake_address = fake.address()
    return render_template('random.html', single_number = number_var, single_address = fake_address)

if __name__ == '__main__':
    app.run(
        debug=True,
        port=8080
    )
```

5. Create a new file ```requirements.txt```
```
faker
pandas
flask
```

6. Create a folder named: templates and inside the folder create 3 different files named ```about.html```, ```base.html```, ```random.html```
In your ```about.html``` put:
```
{% extends "base.html" %} 

{% block content %}

    <section class="mb-6">
        <h2 class="text-xl mb-2">About</h2>
        <p>This is a healthcare application designed to manage patient data efficiently and securely.</p>
    </section>

    <section>
        <h2 class="text-xl mb-2">Features</h2>
        <ul class="list-disc pl-5">
            <li>Secure patient data management</li>
            <li>Easy appointment scheduling</li>
            <li>Interactive dashboards for health metrics</li>
        </ul>
    </section>



{% endblock %}
```
In your ```base.html``` put:
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Azure Deployment App</title>
    
    <!-- Tailwind CSS via CDN -->
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>

<body class="bg-gray-200">

    <header class="bg-blue-600 text-white p-4">
        <h1 class="text-2xl">Azure Deployed Flask App</h1>
        <nav>
            <ul class="flex space-x-4">
                <li><a href="/" class="hover:underline">Home</a></li>
                <li><a href="/about" class="hover:underline">About</a></li>
                <li><a href="/data" class="hover:underline">Data</a></li>
                <li><a href="/random" class="hover:underline">Random Stuff</a></li>
            </ul>
        </nav>
    </header>

    <main class="p-4">

        {% block content %}{% endblock %}

    </main>

    <footer class="bg-blue-600 text-white p-4 mt-6">
        <p>© 2023 My Healthcare App. All Rights Reserved.</p>
    </footer>
</body>

</html>
```
In your ``random.html`` file, put:
```
{% extends "base.html" %} 

{% block content %}

    <section class="mb-6">
        <h2 class="text-xl mb-2">Random Number</h2>
        <p>Below is a random number: </p>
        <p> {{ single_number}} </p>

        <h2 class="text-xl mb-2">Random Address</h2>
        <p>Below is a random address: </p>
        <p> {{ single_address}} </p>
    </section>





{% endblock %}
```
## Deploy Azure App Service steps:

1. In google shell: type in ```curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash```
2. Type in ```Az``` then type in ```az login --use-device-code```
3. Copy the code given and click on the link. Put in the code to authentify.
4. Type ```az account list --output table```
5. Type ```az account set --subscription <subscriptionId>``` and put in the wanted subscriptionID
6. Go to Azure Web Portal and create a new resource group with desired name for group
7. Type ```az group list```
8. Type ```az webapp up --name- <resource group> -flask --runtime PYTHON:3.9 --sku B1``` and change resource group with your resource group name
9. Wait for webapp to be completed
10. Go App services to track deployment. Once completed, Azure link will appear
11. In google shell, to save everything, type in ```git add .```, ```git commit -m <'Message`>```, ```git push```

