import React, { useState } from "react";

const Flex = () => {
  const [formData, setFormData] = useState({
    index: "",
    randomName: "",
    colorName: "",
    boxNo: 0,
  });

  const [boxes, setBoxes] = useState([]);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const newBoxes = Array.from({ length: Number(formData.boxNo) }, (_, i) => ({
      id: i,
      color: "gray", //default color
      text: `Box ${i + 1}`,
    }));
    setBoxes(newBoxes);
  };

  const handleUpdate = (e) => {
    e.preventDefault();
    const index = Number(formData.index);
    if (index >= 0 && index < boxes.length) {
      const updatedBoxes = [...boxes];
      updatedBoxes[index] = {
        ...updatedBoxes[index],
        color: formData.colorName || updatedBoxes[index].color,
        text: formData.randomName || updatedBoxes[index].text,
      };
      setBoxes(updatedBoxes);
    }
  };

  return (
    <div style={{ display: "flex", width: "100vw", height: "100vh" }}>
      {/* left side */}
      <div
        style={{ width: "20%", padding: "10px", borderRight: "2px solid #ccc" }}
      >
        <h3>Enter Details</h3>
        <form onSubmit={handleSubmit}>
          <div>
            <label>Index:</label>
            <input
              type="text"
              name="index"
              value={formData.index}
              onChange={handleChange}
            />
          </div>
          <div>
            <label>Random Name:</label>
            <input
              type="text"
              name="randomName"
              value={formData.randomName}
              onChange={handleChange}
            />
          </div>
          <div>
            <label>Color Name:</label>
            <input
              type="text"
              name="colorName"
              value={formData.colorName}
              onChange={handleChange}
            />
          </div>
          <div>
            <label>Box No:</label>
            <input
              type="number"
              name="boxNo"
              value={formData.boxNo}
              onChange={handleChange}
            />
          </div>
          <button type="submit">Generate Boxes</button>
        </form>
        <button onClick={handleUpdate} style={{ marginTop: "10px" }}>
          Update Box
        </button>
      </div>

      {/* // Right Side Boxes */}
      <div
        style={{
          display: "flex",
          flexWrap: "wrap",
          gap: "2px",
          flex: 1,
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        {boxes.map((box) => (
          <div
            key={box.id}
            style={{
              backgroundColor: box.color,
              color: "white",
              textAlign: "center",
              borderRadius: "5px",
              minWidth: "300px",
              minHeight: "300px",
              flex: "1 1 100px",
              display: "flex",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            {box.text} ({box.id + 1})
          </div>
        ))}
      </div>
    </div>
  );
};

export default Flex;
