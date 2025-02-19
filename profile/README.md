## Hi there 👋



**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)


Creating a complete portfolio and e-commerce website with PDF viewing and a subscription system is a significant project. Below, I will provide a more modern and simplified version of the code structure, including all necessary files and their contents. This example will use React for the frontend and Node.js with Express for the backend.

### Project Structure

```
/portfolio-ecommerce
│
├── /client                  # Frontend (React)
│   ├── /public
│   │   ├── index.html
│   │   └── favicon.ico
│   ├── /src
│   │   ├── App.js
│   │   ├── index.js
│   │   ├── components
│   │   │   ├── Navbar.js
│   │   │   ├── Portfolio.js
│   │   │   ├── PDFViewer.js
│   │   │   ├── Subscription.js
│   │   │   └── ContactForm.js
│   │   ├── pages
│   │   │   ├── Home.js
│   │   │   ├── Product.js
│   │   │   └── MyAccount.js
│   │   └── styles.css
│   └── package.json
│
├── /server                  # Backend (Node.js)
│   ├── /config
│   │   └── db.js
│   ├── /controllers
│   │   ├── authController.js
│   │   ├── pdfController.js
│   │   └── subscriptionController.js
│   ├── /models
│   │   ├── User.js
│   │   ├── PDF.js
│   │   └── Subscription.js
│   ├── /routes
│   │   ├── authRoutes.js
│   │   ├── pdfRoutes.js
│   │   └── subscriptionRoutes.js
│   ├── /middleware
│   │   └── authMiddleware.js
│   ├── server.js
│   └── package.json
│
└── README.md
```

### Frontend Code (React)

#### 1. `client/src/index.js`
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './styles.css';

ReactDOM.render(<App />, document.getElementById('root'));
```

#### 2. `client/src/App.js`
```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import Navbar from './components/Navbar';
import Home from './pages/Home';
import Portfolio from './components/Portfolio';
import Product from './pages/Product';
import MyAccount from './pages/MyAccount';
import Subscription from './components/Subscription';
import ContactForm from './components/ContactForm';

const App = () => {
  return (
    <Router>
      <Navbar />
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/portfolio" component={Portfolio} />
        <Route path="/product/:id" component={Product} />
        <Route path="/my-account" component={MyAccount} />
        <Route path="/subscription" component={Subscription} />
        <Route path="/contact" component={ContactForm} />
      </Switch>
    </Router>
  );
};

export default App;
```

#### 3. `client/src/components/Navbar.js`
```javascript
import React from 'react';
import { Link } from 'react-router-dom';

const Navbar = () => {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/portfolio">Portfolio</Link>
      <Link to="/subscription">Subscription</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
};

export default Navbar;
```

#### 4. `client/src/components/PDFViewer.js`
```javascript
import React from 'react';
import { Document, Page } from 'react-pdf';

const PDFViewer = ({ pdfUrl }) => {
  return (
    <Document file={pdfUrl}>
      <Page pageNumber={1} />
    </Document>
  );
};

export default PDFViewer;
```

#### 5. `client/src/pages/Home.js`
```javascript
import React from 'react';

const Home = () => {
  return (
    <div>
      <h1>Welcome to My Portfolio</h1>
      <p>Explore my work and subscribe for exclusive content.</p>
    </div>
  );
};

export default Home;
```

#### 6. `client/src/pages/Product.js`
```javascript
import React from 'react';
import PDFViewer from '../components/PDFViewer';

const Product = ({ match }) => {
  const pdfUrl = `/path/to/pdf/${match.params.id}`; // Replace with actual PDF URL
  return (
    <div>
      <h2>Product Details</h2>
      <PDFViewer pdfUrl={pdfUrl} />
    </div>
  );
};

export default Product;
```

#### 7. `client/src/pages/MyAccount.js`
```javascript
import React from 'react';

const MyAccount = () => {
  return (
    <div>
      <h2>My Account</h2>
      <p>Manage your subscriptions and account details here.</p>
    </div>
  );
};

export default MyAccount;
```

#### 8. `client/src/components/Subscription.js`
```javascript
import React from 'react';

const Subscription = () => {
  return (
    <div>
      <h2>Subscription Plans</h2>
      <p>Choose a plan to access exclusive content.</p>
      {/* Add subscription options here */}
    </div>
  );
};

export default Subscription;
```

#### 9. `client/src/components/ContactForm.js`
```javascript
import React from 'react';

const ContactForm = () => {
  return (
    <form>
      <h2>Contact Me</h2>
      <input type="text" placeholder="Your Name" required />
      <input type="email" placeholder="Your Email" required />
      <textarea placeholder="Your Message" required></textarea>
      <button type="submit">Send</button>
    </form>
  );
};

export default ContactForm;
```

#### 10. `client/src/styles.css`
```css
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

nav {
  background-color: #333;
  color: white;
  padding: 1rem;
}

nav a {
  color: white;
  margin: 0 1rem;
  text-decoration: none;
}

h1, h2 {
  color: #333;
}
```

### Backend Code (Node.js)

#### 1. `server/server.js`
```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const authRoutes = require('./routes/authRoutes');
const pdfRoutes = require('./routes/pdfRoutes');
const subscriptionRoutes = require('./routes/subscriptionRoutes');

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect('mongodb://localhost:27017/portfolio-ecommerce', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

app.use('/api/auth', authRoutes);
app.use('/api/pdfs', pdfRoutes);
app.use('/api/subscriptions', subscriptionRoutes);

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

#### 2. `server/models/User.js`
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  username: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  subscription: { type: mongoose.Schema.Types.ObjectId, ref: 'Subscription' },
});

module.exports = mongoose.model('User ', userSchema);
```

Certainly! Let's continue with the backend code for the `PDF.js` model and the rest of the necessary files.

### 3. `server/models/PDF.js`
```javascript
const mongoose = require('mongoose');

const pdfSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String, required: true },
  filePath: { type: String, required: true }, // Path to the PDF file
  price: { type: Number, required: true },
});

module.exports = mongoose.model('PDF', pdfSchema);
```

### 4. `server/models/Subscription.js`
```javascript
const mongoose = require('mongoose');

const subscriptionSchema = new mongoose.Schema({
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User ' },
  plan: { type: String, required: true }, // e.g., 'monthly', 'yearly'
  startDate: { type: Date, default: Date.now },
  endDate: { type: Date, required: true },
});

module.exports = mongoose.model('Subscription', subscriptionSchema);
```

### 5. `server/controllers/authController.js`
```javascript
const User = require('../models/User');
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

exports.register = async (req, res) => {
  const { username, email, password } = req.body;
  const hashedPassword = await bcrypt.hash(password, 10);
  const user = new User({ username, email, password: hashedPassword });
  await user.save();
  res.status(201).json({ message: 'User  registered successfully' });
};

exports.login = async (req, res) => {
  const { email, password } = req.body;
  const user = await User.findOne({ email });
  if (!user || !(await bcrypt.compare(password, user.password))) {
    return res.status(401).json({ message: 'Invalid credentials' });
  }
  const token = jwt.sign({ id: user._id }, 'your_jwt_secret', { expiresIn: '1h' });
  res.json({ token });
};
```

### 6. `server/controllers/pdfController.js`
```javascript
const PDF = require('../models/PDF');

exports.getAllPDFs = async (req, res) => {
  const pdfs = await PDF.find();
  res.json(pdfs);
};

exports.getPDFById = async (req, res) => {
  const pdf = await PDF.findById(req.params.id);
  if (!pdf) return res.status(404).json({ message: 'PDF not found' });
  res.json(pdf);
};
```

### 7. `server/controllers/subscriptionController.js`
```javascript
const Subscription = require('../models/Subscription');

exports.createSubscription = async (req, res) => {
  const { userId, plan, endDate } = req.body;
  const subscription = new Subscription({ user: userId, plan, endDate });
  await subscription.save();
  res.status(201).json(subscription);
};

exports.getUser Subscription = async (req, res) => {
  const subscription = await Subscription.findOne({ user: req.params.userId });
  if (!subscription) return res.status(404).json({ message: 'Subscription not found' });
  res.json(subscription);
};
```

### 8. `server/routes/authRoutes.js`
```javascript
const express = require('express');
const { register, login } = require('../controllers/authController');
const router = express.Router();

router.post('/register', register);
router.post('/login', login);

module.exports = router;
```

### 9. `server/routes/pdfRoutes.js`
```javascript
const express = require('express');
const { getAllPDFs, getPDFById } = require('../controllers/pdfController');
const router = express.Router();

router.get('/', getAllPDFs);
router.get('/:id', getPDFById);

module.exports = router;
```

### 10. `server/routes/subscriptionRoutes.js`
```javascript
const express = require('express');
const { createSubscription, getUser Subscription } = require('../controllers/subscriptionController');
const router = express.Router();

router.post('/', createSubscription);
router.get('/:userId', getUser Subscription);

module.exports = router;
```

### 11. `server/middleware/authMiddleware.js`
```javascript
const jwt = require('jsonwebtoken');

const authMiddleware = (req, res, next) => {
  const token = req.headers['authorization'];
  if (!token) return res.status(403).send('A token is required for authentication');

  try {
    const decoded = jwt.verify(token, 'your_jwt_secret');
    req.user = decoded;
  } catch (err) {
    return res.status(401).send('Invalid Token');
  }
  return next();
};

module.exports = authMiddleware;
```

### 12. `server/config/db.js`
```javascript
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect('mongodb://localhost:27017/portfolio-ecommerce', {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log('MongoDB connected');
  } catch (error) {
    console.error('MongoDB connection error:', error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### 13. `server/package.json`
```json
{
  "name": "portfolio-ecommerce",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "bcrypt": "^5.0.1",
    "cors": "^2.8.5",
    "express": "^4.17.1",
    "jsonwebtoken": "^8.5.1",
    "mongoose": "^5.10.9"
  },
  "devDependencies": {
    "nodemon": "^2.0.4"
  }
}
```

### 14. `client/package.json`
```json
{
  "name": "portfolio-ecommerce-client",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-pdf": "^5.5.0",
    "react-router-dom": "^5.2.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### 15. `README.md`
```markdown
# Portfolio E-commerce Website

This is a simple portfolio and e-commerce website that allows users to view and purchase PDF documents. It includes user authentication, subscription management, and a PDF viewer.

## Getting Started

### Prerequisites

- Node.js
- MongoDB

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/portfolio-ecommerce.git
   cd portfolio-ecommerce
   ```

2. Install server dependencies:
   ```bash
   cd server
   npm install
   ```

3. Install client dependencies:
   ```bash
   cd client
   npm install
   ```

### Running the Application

1. Start the backend server:
   ```bash
   cd server
   npm run dev
   ```

2. Start the frontend application:
   ```bash
   cd client
   npm start
   ```

### Features

- User registration and login
- Subscription plans
- PDF viewing
- Portfolio showcase
- Contact form

### License

This project is licensed under the MIT License.
```

### Final Steps

