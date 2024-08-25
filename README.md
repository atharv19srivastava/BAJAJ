# BAJAJ
npx create-react-app your-app-name
cd your-app-name
npx create-next-app@latest your-app-name
cd your-app-name
import React, { useState } from 'react';

function App() {
  const [jsonInput, setJsonInput] = useState('');
  const [error, setError] = useState('');
  const [response, setResponse] = useState(null);
  const [showDropdown, setShowDropdown] = useState(false);
  const [selectedOptions, setSelectedOptions] = useState([]);

  const handleSubmit = async () => {
    try {
      const parsedJson = JSON.parse(jsonInput);
      setError('');
      const res = await fetch('YOUR_BACKEND_API_URL', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(parsedJson),
      });
      const data = await res.json();
      setResponse(data);
      setShowDropdown(true);
    } catch (err) {
      setError('Invalid JSON format.');
    }
  };

  const handleDropdownChange = (e) => {
    const { value } = e.target;
    setSelectedOptions([...selectedOptions, value]);
  };

  return (
    <div>
      <h1>Your Roll Number</h1>
      <textarea 
        value={jsonInput} 
        onChange={(e) => setJsonInput(e.target.value)} 
        placeholder="Enter JSON" 
      />
      <button onClick={handleSubmit}>Submit</button>
      {error && <p style={{ color: 'red' }}>{error}</p>}
      {showDropdown && (
        <select onChange={handleDropdownChange} multiple>
          <option value="alphabets">Alphabets</option>
          <option value="numbers">Numbers</option>
          <option value="highest-lowercase">Highest lowercase alphabet</option>
        </select>
      )}
      {response && (
        <div>
          {/* Render response based on selected options */}
          {selectedOptions.includes('alphabets') && <p>Alphabets: {response.alphabets}</p>}
          {selectedOptions.includes('numbers') && <p>Numbers: {response.numbers}</p>}
          {selectedOptions.includes('highest-lowercase') && <p>Highest Lowercase Alphabet: {response.highestLowercase}</p>}
        </div>
      )}
    </div>
  );
}

export default App;
import { useEffect } from 'react';

useEffect(() => {
  document.title = '21BEC0267';
}, []);
npm start
