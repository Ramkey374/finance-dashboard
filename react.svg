import { useState } from "react";
import { transactions } from "./data/mockData";
import { PieChart, Pie, Tooltip, LineChart, Line, XAxis, YAxis, CartesianGrid,Legend } from "recharts";
function App() {
  const [search, setSearch] = useState("");
  const [role, setRole] = useState("viewer");
  const [data, setData] = useState(transactions);
const [category, setCategory] = useState("");
const [amount, setAmount] = useState("");
const [type, setType] = useState("income");
const deleteTransaction = (id) => {
  setData(data.filter((t) => t.id !== id));
};
const addTransaction = () => {
  const newItem = {
    id: Date.now(),
    category: category,
    amount: Number(amount),
    type: type
  };

  setData([...data, newItem]);
};

  // Filter data
  const filtered = data.filter((t) =>
    t.category.toLowerCase().includes(search.toLowerCase())
  );

  // Calculations
  const income = data
    .filter((t) => t.type === "income")
    .reduce((sum, t) => sum + t.amount, 0);

  const expense = data
    .filter((t) => t.type === "expense")
    .reduce((sum, t) => sum + t.amount, 0);
const balance = income - expense;
const chartData = filtered.map((t, index) => ({
  name: `T${index + 1}`,
  income: t.type === "income" ? t.amount : 0,
  expense: t.type === "expense" ? t.amount : 0,
}));
return (
    <div style={{ padding: "20px",color:"white" }}>
      <h1>Finance Dashboard</h1>
      <div style={{ marginTop: "20px" }}></div>

      {/* ROLE SWITCH */}
      <select onChange={(e) => setRole(e.target.value)}>
        <option value="viewer">Viewer</option>
        <option value="admin">Admin</option>
      </select>

      {/* SEARCH */}
      <input
  placeholder="Search category..."
  style={{ marginLeft: "10px", padding: "5px" }}
/>

<input
  type="number"
  placeholder="Amount"
  onChange={(e) => setAmount(e.target.value)}
/>

<select onChange={(e) => setType(e.target.value)}>
  <option value="income">Income</option>
  <option value="expense">Expense</option>
</select>

<button 
  onClick={addTransaction}
  style={{ marginLeft: "10px", padding: "5px" }}
>
  Add Transaction
</button>
      {/* CARDS */}
      <div style={{ display: "flex", gap: "20px", marginTop: "20px" }}>
        <div>Income: ₹{income}</div>
        <div>Expense: ₹{expense}</div>
        <div>Balance: ₹{balance}</div>
      </div>

      <hr />
      <PieChart width={300} height={300}>
  <Pie
    data={[
      { name: "Income", value: income },
      { name: "Expense", value: expense }
    ]}
    dataKey="value"
    cx="50%"
    cy="50%"
    outerRadius={80}
    fill="#8884d8"
    label
  />
  <Tooltip />
</PieChart>
{/* Line Chart UI */}
<h3 style={{ marginTop: "30px" }}>Line Chart</h3>

<LineChart width={600} height={300} data={chartData}>
  <CartesianGrid strokeDasharray="3 3" />
  <XAxis dataKey="name" />
  <YAxis />
  <Tooltip />
  <Legend />
  <Line type="monotone" dataKey="income" stroke="#82ca9d" />
  <Line type="monotone" dataKey="expense" stroke="#ff7300" />
</LineChart>
{/* Insights Section */}
<h3 style={{ marginTop: "20px" }}>Insights</h3>
<p>Total Transactions: {data.length}</p>
<p>Total Income: ₹{income}</p>
<p>Total Expense: ₹{expense}</p>
<p>Balance: ₹{balance}</p>
      {/* TRANSACTIONS */}
      {filtered.map((t) => (
  <div 
  key={t.id}
  style={{
    marginTop: "10px",
    borderBottom: "1px solid gray",
    padding: "5px",
  }}
>
    {t.category} - ₹{t.amount}

    {role === "admin" && (
      <button onClick={() => deleteTransaction(t.id)}>
        Delete
      </button>
    )}
  </div>
))}

      {/* ADMIN BUTTON */}
      {role === "admin" && (
        <button style={{ marginTop: "20px" }}>
          Add Transaction
        </button>
      )}
    </div>
  );
}

export default App;