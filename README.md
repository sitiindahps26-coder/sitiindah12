
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Sistem Informasi Profil</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f0f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      background: #fff;
      padding: 20px 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      width: 350px;
    }

    h1, h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    #profile-view, #profile-edit {
      text-align: center;
    }

    img#profile-pic {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      object-fit: cover;
      margin-bottom: 15px;
    }

    input[type="text"],
    input[type="email"],
    input[type="file"] {
      width: 100%;
      padding: 8px;
      margin-bottom: 12px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    button {
      padding: 8px 16px;
      border: none;
      background-color: #4CAF50;
      color: white;
      border-radius: 4px;
      cursor: pointer;
      margin-top: 10px;
    }

    button:hover {
      background-color: #45a049;
    }

    .form-buttons {
      display: flex;
      justify-content: space-between;
    }

    .form-buttons button {
      width: 48%;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Profil Pengguna</h1>

    <div id="profile-view">
      <img id="profile-pic" src="https://via.placeholder.com/100" alt="Foto Profil">
      <p><strong>Nama:</strong> <span id="user-name">John Doe</span></p>
      <p><strong>Email:</strong> <span id="user-email">john.doe@example.com</span></p>
      <button onclick="editProfile()">Edit Profil</button>
    </div>

    <div id="profile-edit" style="display: none;">
      <h2>Edit Profil</h2>
      <form id="edit-form">
        <label for="edit-name">Nama:</label>
        <input type="text" id="edit-name" required>

        <label for="edit-email">Email:</label>
        <input type="email" id="edit-email" required>

        <label for="edit-photo">Foto Profil:</label>
        <input type="file" id="edit-photo" accept="image/*">

        <div class="form-buttons">
          <button type="submit">Simpan</button>
          <button type="button" onclick="cancelEdit()">Batal</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    // Data awal pengguna
    let profileData = {
      name: "John Doe",
      email: "john.doe@example.com",
      photo: "https://via.placeholder.com/100"
    };

    // Tampilkan data profil di tampilan utama
    function displayProfile() {
      document.getElementById("user-name").textContent = profileData.name;
      document.getElementById("user-email").textContent = profileData.email;
      document.getElementById("profile-pic").src = profileData.photo;
    }

    // Buka form edit profil
    function editProfile() {
      document.getElementById("profile-view").style.display = "none";
      document.getElementById("profile-edit").style.display = "block";

      document.getElementById("edit-name").value = profileData.name;
      document.getElementById("edit-email").value = profileData.email;
    }

    // Batalkan edit
    function cancelEdit() {
      document.getElementById("profile-edit").style.display = "none";
      document.getElementById("profile-view").style.display = "block";
    }

    // Simpan perubahan
    document.getElementById("edit-form").addEventListener("submit", function(event) {
      event.preventDefault();

      // Ambil nilai input
      profileData.name = document.getElementById("edit-name").value;
      profileData.email = document.getElementById("edit-email").value;

      const photoInput = document.getElementById("edit-photo");
      if (photoInput.files && photoInput.files[0]) {
        const reader = new FileReader();
        reader.onload = function(e) {
          profileData.photo = e.target.result;
          updateProfile();
        };
        reader.readAsDataURL(photoInput.files[0]);
      } else {
        updateProfile();
      }
    });

    function updateProfile() {
      displayProfile();
      cancelEdit();
    }

    // Tampilkan profil saat halaman pertama kali dimuat
    displayProfile();
  </script>
</body>
</html>


