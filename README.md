# X-HEC MLOps Class Introductory Workshop


1. Form groups of 3 to 4 persons, ideally with complementary skills (data, math, SE,...)
   - Fill group file

2. Access your AWS machine via VS Code

   - Download VS Code
   - Open « Remote Explorer »
   - Ask for your machine's Public IPv4 URL & your key set 
   - Add SSH connection (ou  can test you ssh command in your terminal to see if there are any errors)

Note : 
- Add Windows Instructions ( ssh -i "path/to/keypair" ec2-user@{url-name} )
- VS Code tutorial ( add plugin, go to Tunnel - SSH, Click on + )
- Explain the « coding rules »,  eg. {}
  
```
sudo  chmod 400 x-hec-key-pair.pem
ssh-add x-hec-key-pair.pem
ssh -i x-hec-key-pair.pem ec2-user@{url-name}
```

3. Create a git repo

   - Create a git account, star the repository
   - Create a repo for you group
  
```
mkdir {group_name}
cd {group_name}
git clone (fork?) ...
cd [REPO NAME]
```

4. Create a Python Django App

- Create a conda environment

```
conda create -n {group_name} python=3.8
conda activate {group_name}
```

- Create a django app
<!-- 
1. Install django ( pip install django djangorestframework )
2. django-admin startproject prepera_ai_api
-->

- Deploy locally your django App

<!-- 
python manage.py runserver
-->

- Create your first API Endpoint :  GET Call on /health/ that returns healthy 200

1. Create a view
2. Configure your URLs
3. Check Local Host

<!-- 
in views.py : 
from django.http import JsonResponse

def health_check(request):
    # This can be expanded in the future if you want to check database connectivity, etc.
    return JsonResponse({'status': 'healthy'}, status=200)

in urls.py : 
urlpatterns = [
    path('admin/', admin.site.urls),
    path('health/', views.health_check, name='health_check'),
]
-->

5. Create an API Call with a Gen AI Component : Answering questions with HuggingFace's Inference Points.

- Create a new view (GET) and url access
- Ask for the API Key and URL
- Add a call to HF Generate
- Debug & deploy

<!-- 
in views.py : 
from rest_framework.response import Response

MODEL_API_URL = "https://fftj4uc02355sar0.us-east-1.aws.endpoints.huggingface.cloud"

headers = {
    "Authorization": "Bearer {token}",
    "Content-Type": "application/json"
}

# Function to query the HuggingFace model
def query(api_url, payload):
    payload = clean_invalid_floats(payload)
    response = requests.post(api_url, headers=headers, json=payload)
    return response.json()

# Function to handle the API call loop for text generation
def get_model_response(api_url, prompt):

    concatenated_text = ""
    
    for _ in range(10):
        response = query(api_url, {"inputs": prompt})
        text_chunk = response[0].get('generated_text', "")
        if not text_chunk:
            break
        
        concatenated_text += " "
        concatenated_text += text_chunk
        prompt += text_chunk  
    return concatenated_text

@api_view(['GET'])
def question_answered( request ):

   prompt = request.GET.get('question', "What's the question ?")

   base_response = get_model_response(MODEL_API_URL, prompt)
   
   return Response({"output": base_response})

in urls.py : 
-->














