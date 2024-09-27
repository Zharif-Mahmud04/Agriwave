const express = require("express");
const cors = require("cors");
const app = express();

const { MongoClient, ServerApiVersion, ObjectId } = require("mongodb");
const port = process.env.PORT || 5000;
require("dotenv").config();

//middleware
app.use(cors());
app.use(express.json());

//connect mongodb

const uri = `mongodb+srv://admin:admin@cluster0.asru0.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0`;
const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverApi: ServerApiVersion.v1,
});

async function run() {
  const userCollection = client.db("agriwave").collection("user");
  const fieldDataCollection = client.db("agriwave").collection("fieldData");
  const continentCollection = client.db("agriwave").collection("continent");
  const countriesCollection = client.db("agriwave").collection("countries");

  try {
    app.get("/user", async (req, res) => {
      const query = {};
      const results = await userCollection.find(query).toArray();
      res.send(results);
    });

    app.get("/fielddata", async (req, res) => {
      const query = {};
      const results = await fieldDataCollection.find(query).toArray();
      res.send(results);
    });

    app.get("/continent", async (req, res) => {
      const query = {};
      const results = await continentCollection.find(query).toArray();
      res.send(results);
    });

    app.get("/fielddata/:id", async (req, res) => {
      const id = req.params.id;
      console.log(id);

      const query = { country: id };
      const results = await fieldDataCollection.find(query).toArray();
      res.send(results);
    });

    app.get("/countries/:id", async (req, res) => {
      const id = req.params.id;
      const intId = parseInt(id);
      const query = { continentId: intId };
      const results = await countriesCollection.find(query).toArray();
      res.send(results);
    });

    app.post("/user", async (req, res) => {
      const query = req.body;
      const results = await userCollection.insertOne(query);
      res.send(results);
      console.log(results);
    });

    app.post("/fielddata", async (req, res) => {
      const query = req.body;
      const results = await fieldDataCollection.insertOne(query);
      res.send(results);
    });
  } finally {
  }
}

run().catch((err) => console.log(err));

app.get("/", (req, res) => {
  res.send(`Agriwave server is running`);
});

app.listen(port, () => {
  console.log(`Agriwave is running on ${port}`);
});
