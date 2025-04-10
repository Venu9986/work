from flask import Flask
import os
import getpass
from datetime import datetime
import pytz
import subprocess

app = Flask(__name__)

@app.route("/htop")
def htop():
    name = "Your Full Name"
    username = getpass.getuser()
    
    ist = pytz.timezone('Asia/Kolkata')
    current_time = datetime.now(ist).strftime("%Y-%m-%d %H:%M:%S %Z")
    
    top_output = subprocess.getoutput("top -b -n 1")
    
    return f"""
    <h2>Name: {name}</h2>
    <h2>Username: {username}</h2>
    <h2>Server Time (IST): {current_time}</h2>
    <pre>{top_output}</pre>
    """

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
