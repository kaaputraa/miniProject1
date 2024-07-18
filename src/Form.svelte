<script>
  let kodam = "";

  document.addEventListener("DOMContentLoaded", function () {
    const button = document.querySelector("button.cariKodam");
    const input = document.querySelector("input.input");
    const kodamNama = document.getElementById("kodamNama");

    button.addEventListener("click", function () {
      const nama = input.value.trim();
      if (nama === "") {
        return;
      }
      fetchKodamName(nama);
    });

    function fetchKodamName(name) {
      const url =
        "https://pokeapi.co/api/v2/pokemon-species/?offset=0&limit=20";

      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          const results = data.results;
          const randomIndex = Math.floor(Math.random() * results.length);
          kodam = results[randomIndex].name;
          kodamNama.innerHTML = `<b>"${kodam}"</b>`;
        })
        .catch((error) => {
          console.error("Error fetching Kodam name:", error);
          kodamNama.innerHTML = `<b>${name} - Error fetching Kodam name</b>`;
        });
    }
  });
</script>

<main>
  <div class="form">
    <div class="form-group">
      <div class="header"><h1>CEK KODAM DISINI</h1></div>
      <div class="namaKodam"><p id="kodamNama"><b>"{kodam}"</b></p></div>
      <input class="input" type="text" placeholder="Masukkan Nama Anda" />
      <button class="cariKodam">Temukan</button>
    </div>
  </div>
</main>

<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .header {
    color: white;
  }

  .namaKodam {
    font-size: 22px;
    padding: 10%;
    color: white;
    text-decoration: underline;
  }

  .form {
    max-width: 400px;
    height: 400px;
    margin: auto;
    margin-top: 160px;
    border-radius: 6px;
    background-color: rgb(0, 140, 255);
    box-shadow:
      0 4px 8px 0 rgba(54, 54, 54, 0.246),
      0 6px 20px 0 rgba(54, 54, 54, 0.168);
  }
  .form-group {
    max-width: 350px;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 22px;
    margin: auto;
  }

  input.input {
    width: 90%;
    height: 38px;
    background-color: white;
    border-radius: 6px;
    text-align: center;
    border: 0;
  }

  button.cariKodam {
    width: 90%;
    height: 38px;
    border-radius: 6px;
    background-color: rgb(54, 54, 54);
    color: white;
    border: 0;
  }
</style>
