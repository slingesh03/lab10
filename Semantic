// Step 1: Switch to Legal Search Database
use legalDB;

// Step 2: Insert Legal Documents with pre-computed Vector Embeddings
db.legalDocs.insertMany([
  {
    docId: "LEG-2026-88",
    title: "Non-Disclosure Agreement Clause 4",
    clauseType: "Confidentiality",
    text: "Receiving party agrees not to disclose proprietary trade secrets to third parties.",
    // Simplified 4-dimensional vector embedding representation
    embedding: [0.12, -0.45, 0.88, 0.31]
  },
  {
    docId: "LEG-2026-92",
    title: "Employment Contract Termination Clause",
    clauseType: "Termination",
    text: "Either party may terminate this agreement with a 30-day prior written notice.",
    embedding: [-0.65, 0.22, 0.05, 0.91]
  }
]);

// Step 3: Semantic Search Aggregation (Simulated KNN Vector Search Pipeline)
// Input query embedding for "keeping secrets hidden": [0.10, -0.42, 0.85, 0.30]
db.legalDocs.aggregate([
  {
    $vectorSearch: {
      index: "vector_index",
      path: "embedding",
      queryVector: [0.10, -0.42, 0.85, 0.30],
      numCandidates: 10,
      limit: 1
    }
  },
  {
    $project: {
      _id: 0,
      title: 1,
      clauseType: 1,
      text: 1,
      score: { $meta: "vectorSearchScore" }
    }
  }
]);
