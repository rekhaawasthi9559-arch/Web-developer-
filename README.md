<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Notes App</title>
  <link href="[fonts.googleapis.com](https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap)" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
      min-height: 100vh;
      padding: 40px 20px;
    }

    .container {
      max-width: 1200px;
      margin: auto;
    }

    header {
      text-align: center;
      margin-bottom: 40px;
    }

    h1 {
      font-size: 2.5rem;
      font-weight: 700;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 8px;
    }

    .subtitle {
      color: rgba(255, 255, 255, 0.6);
      font-size: 1rem;
    }

    .top-bar {
      display: flex;
      gap: 12px;
      margin-bottom: 32px;
      flex-wrap: wrap;
    }

    #searchInput {
      flex: 1;
      min-width: 200px;
      padding: 16px 20px;
      border: none;
      border-radius: 16px;
      font-size: 15px;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      color: white;
      outline: none;
      transition: all 0.3s ease;
    }

    #searchInput::placeholder {
      color: rgba(255, 255, 255, 0.5);
    }

    #searchInput:focus {
      background: rgba(255, 255, 255, 0.15);
      box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.3);
    }

    #addNoteBtn {
      padding: 16px 28px;
      border: none;
      border-radius: 16px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      font-weight: 600;
      font-size: 15px;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    #addNoteBtn:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
    }

    #addNoteBtn:active {
      transform: translateY(0);
    }

    .stats {
      display: flex;
      gap: 20px;
      margin-bottom: 24px;
      flex-wrap: wrap;
    }

    .stat-card {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      padding: 16px 24px;
      border-radius: 12px;
      color: white;
    }

    .stat-card .number {
      font-size: 1.5rem;
      font-weight: 700;
      color: #667eea;
    }

    .stat-card .label {
      font-size: 0.85rem;
      color: rgba(255, 255, 255, 0.6);
    }

    #notesContainer {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 24px;
    }

    .note {
      background: rgba(255, 255, 255, 0.95);
      padding: 24px;
      border-radius: 20px;
      position: relative;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
      transition: all 0.3s ease;
      animation: fadeIn 0.4s ease;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .note:hover {
      transform: translateY(-5px);
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
    }

    .note-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 16px;
    }

    .note-color-picker {
      display: flex;
      gap: 6px;
    }

    .color-dot {
      width: 20px;
      height: 20px;
      border-radius: 50%;
      cursor: pointer;
      transition: transform 0.2s ease;
      border: 2px solid transparent;
    }

    .color-dot:hover {
      transform: scale(1.2);
    }

    .color-dot.active {
      border-color: #333;
    }

    .note textarea {
      width: 100%;
      height: 160px;
      border: none;
      resize: none;
      outline: none;
      font-size: 15px;
      line-height: 1.6;
      color: #333;
      background: transparent;
      font-family: 'Inter', sans-serif;
    }

    .note textarea::placeholder {
      color: #aaa;
    }

    .note-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 16px;
      padding-top: 16px;
      border-top: 1px solid rgba(0, 0, 0, 0.08);
    }

    .timestamp {
      font-size: 12px;
      color: #888;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .note-buttons {
      display: flex;
      gap: 8px;
    }

    .btn {
      border: none;
      padding: 10px 16px;
      border-radius: 10px;
      cursor: pointer;
      font-weight: 600;
      font-size: 13px;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .save-btn {
      background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
      color: white;
    }

    .save-btn:hover {
      box-shadow: 0 5px 20px rgba(17, 153, 142, 0.4);
      transform: translateY(-2px);
    }

    .delete-btn {
      background: linear-gradient(135deg, #eb3349 0%, #f45c43 100%);
      color: white;
    }

    .delete-btn:hover {
      box-shadow: 0 5px 20px rgba(235, 51, 73, 0.4);
      transform: translateY(-2px);
    }

    .empty-state {
      text-align: center;
      padding: 60px 20px;
      color: rgba(255, 255, 255, 0.6);
    }

    .empty-state svg {
      width: 80px;
      height: 80px;
      margin-bottom: 20px;
      opacity: 0.5;
    }

    .empty-state h3 {
      font-size: 1.25rem;
      margin-bottom: 8px;
      color: rgba(255, 255, 255, 0.8);
    }

    .toast {
      position: fixed;
      bottom: 30px;
      right: 30px;
      background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
      color: white;
      padding: 16px 24px;
      border-radius: 12px;
      font-weight: 600;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      transform: translateY(100px);
      opacity: 0;
      transition: all 0.3s ease;
      z-index: 1000;
    }

    .toast.show {
      transform: translateY(0);
      opacity: 1;
    }

    @media (max-width: 600px) {
      h1 {
        font-size: 1.8rem;
      }
      
      .note {
        padding: 20px;
      }
      
      .top-bar {
        flex-direction: column;
      }
      
      #addNoteBtn {
        justify-content: center;
      }
    }
  </style>
</head>

<body>

  <div class="container">
    <header>
      <h1>✨ Notes App</h1>
      <p class="subtitle">Capture your thoughts, ideas, and inspirations</p>
    </header>

    <div class="stats">
      <div class="stat-card">
        <div class="number" id="noteCount">0</div>
        <div class="label">Total Notes</div>
      </div>
      <div class="stat-card">
        <div class="number" id="charCount">0</div>
        <div class="label">Characters</div>
      </div>
    </div>

    <div class="top-bar">
      <input type="text" id="searchInput" placeholder="🔍 Search your notes..." />
      <button id="addNoteBtn">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
          <line x1="12" y1="5" x2="12" y2="19"></line>
          <line x1="5" y1="12" x2="19" y2="12"></line>
        </svg>
        Add Note
      </button>
    </div>

    <div id="notesContainer"></div>
  </div>

  <div class="toast" id="toast">Note saved!</div>

  <script>
    const addNoteBtn = document.getElementById("addNoteBtn");
    const notesContainer = document.getElementById("notesContainer");
    const searchInput = document.getElementById("searchInput");
    const noteCountEl = document.getElementById("noteCount");
    const charCountEl = document.getElementById("charCount");
    const toast = document.getElementById("toast");

    const colors = ["#ffffff", "#fff3cd", "#d4edda", "#cce5ff", "#f8d7da", "#e2d5f1"];

    let notes = JSON.parse(localStorage.getItem("notes")) || [];

    function showToast(message) {
      toast.textContent = message;
      toast.classList.add("show");
      setTimeout(() => toast.classList.remove("show"), 2500);
    }

    function saveToLocalStorage() {
      localStorage.setItem("notes", JSON.stringify(notes));
    }

    function updateStats() {
      noteCountEl.textContent = notes.length;
      const totalChars = notes.reduce((sum, note) => sum + note.text.length, 0);
      charCountEl.textContent = totalChars.toLocaleString();
    }

    function renderNotes(filteredNotes = notes) {
      notesContainer.innerHTML = "";
      updateStats();

      if (filteredNotes.length === 0) {
        notesContainer.innerHTML = `
          <div class="empty-state" style="grid-column: 1 / -1;">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
            </svg>
            <h3>No notes yet</h3>
            <p>Click "Add Note" to create your first note!</p>
          </div>
        `;
        return;
      }

      filteredNotes.forEach((note, index) => {
        const actualIndex = notes.indexOf(note);
        const noteDiv = document.createElement("div");
        noteDiv.classList.add("note");
        noteDiv.style.background = note.color || "#ffffff";

        noteDiv.innerHTML = `
          <div class="note-header">
            <div class="note-color-picker">
              ${colors.map(color => `
                <div class="color-dot ${note.color === color ? 'active' : ''}" 
                     style="background: ${color}; ${color === '#ffffff' ? 'border: 1px solid #ddd;' : ''}"
                     data-color="${color}"></div>
              `).join('')}
            </div>
          </div>
          <textarea placeholder="Write something amazing...">${note.text}</textarea>
          <div class="note-footer">
            <div class="timestamp">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"></circle>
                <polyline points="12,6 12,12 16,14"></polyline>
              </svg>
              ${note.date}
            </div>
            <div class="note-buttons">
              <button class="btn save-btn">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="20,6 9,17 4,12"></polyline>
                </svg>
                Save
              </button>
              <button class="btn delete-btn">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="3,6 5,6 21,6"></polyline>
                  <path d="M19,6v14a2,2,0,0,1-2,2H7a2,2,0,0,1-2-2V6M8,6V4a2,2,0,0,1,2-2h4a2,2,0,0,1,2,2V6"></path>
                </svg>
                Delete
              </button>
            </div>
          </div>
        `;

        const textarea = noteDiv.querySelector("textarea");
        const saveBtn = noteDiv.querySelector(".save-btn");
        const deleteBtn = noteDiv.querySelector(".delete-btn");
        const colorDots = noteDiv.querySelectorAll(".color-dot");

        colorDots.forEach(dot => {
          dot.addEventListener("click", () => {
            notes[actualIndex].color = dot.dataset.color;
            saveToLocalStorage();
            renderNotes(searchInput.value ? filteredNotes : notes);
          });
        });

        textarea.addEventListener("input", () => {
          notes[actualIndex].text = textarea.value;
          notes[actualIndex].date = new Date().toLocaleString();
          saveToLocalStorage();
          updateStats();
        });

        saveBtn.addEventListener("click", () => {
          notes[actualIndex].text = textarea.value;
          notes[actualIndex].date = new Date().toLocaleString();
          saveToLocalStorage();
          showToast("✓ Note saved successfully!");
          renderNotes(searchInput.value ? filteredNotes : notes);
        });

        deleteBtn.addEventListener("click", () => {
          noteDiv.style.animation = "fadeIn 0.3s ease reverse";
          setTimeout(() => {
            notes.splice(actualIndex, 1);
            saveToLocalStorage();
            renderNotes();
            showToast("🗑️ Note deleted");
          }, 250);
        });

        notesContainer.appendChild(noteDiv);
      });
    }

    addNoteBtn.addEventListener("click", () => {
      notes.unshift({
        text: "",
        date: new Date().toLocaleString(),
        color: "#ffffff"
      });
      saveToLocalStorage();
      renderNotes();
      
      setTimeout(() => {
        const firstTextarea = notesContainer.querySelector("textarea");
        if (firstTextarea) firstTextarea.focus();
      }, 100);
    });

    searchInput.addEventListener("input", () => {
      const searchText = searchInput.value.toLowerCase();
      const filteredNotes = notes.filter(note =>
        note.text.toLowerCase().includes(searchText)
      );
      renderNotes(filteredNotes);
    });

    renderNotes();
  </script>

</body>
</html>
