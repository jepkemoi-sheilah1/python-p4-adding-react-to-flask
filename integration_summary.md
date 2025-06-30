# React and Flask Integration Summary

This project demonstrates how to integrate a React frontend with a Flask backend to build a full-stack web application.

## Project Structure

- `client/`: Contains the React frontend application.
- `server/`: Contains the Flask backend application.

## Running the Application

1. **Backend (Flask) Setup:**

   Open a terminal and navigate to the `server/` directory:

   ```bash
   pipenv install && pipenv shell
   export FLASK_APP=app.py
   export FLASK_RUN_PORT=5555
   flask db upgrade
   python seed.py
   python app.py
   ```

   This will start the Flask server on port 5555.

2. **Frontend (React) Setup:**

   Open another terminal and navigate to the `client/` directory:

   ```bash
   npm install
   npm start
   ```

   This will start the React development server, usually on port 3000, and open the app in your browser.

## How React and Flask Work Together

- The React app fetches data from the Flask backend API using the `fetch()` function.
- In `client/src/components/App.js`, the `useEffect` hook fetches messages from `http://127.0.0.1:5555/messages` on initial render and stores them in state.
- React components like `NewMessage` send POST requests to the Flask backend to create new messages.
- Flask handles API requests in `server/app.py` with routes for GET, POST, PATCH, and DELETE on `/messages` and `/messages/<id>`.
- Flask uses Flask-CORS (`CORS(app)`) to allow cross-origin requests from the React frontend, which runs on a different port.

## Key Code Highlights

### React (App.js)

```javascript
useEffect(() => {
  fetch("http://127.0.0.1:5555/messages")
    .then((r) => r.json())
    .then((messages) => setMessages(messages));
}, []);
```

### Flask (app.py)

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route('/messages', methods=['GET', 'POST'])
def messages():
    # Handle GET and POST requests
```

## Notes

- Ensure both servers are running simultaneously for the app to function correctly.
- The React app runs on port 3000 by default, and Flask runs on port 5555.
- CORS is essential to allow the React app to communicate with the Flask API.

## Next Steps

- You can extend the app by adding more features or improving UI/UX.
- If you encounter any issues or want to add new functionality, feel free to ask for assistance.

---

This summary should help you understand and run the React-Flask full-stack application effectively.
