
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Provisión Silvana Pesca</title>
<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@400;700&display=swap" rel="stylesheet">
<style>
    body { font-family: 'Poppins', sans-serif; margin: 0; padding: 0; background: linear-gradient(rgba(0, 30, 60, 0.7), rgba(0, 30, 60, 0.7)), url('https://images.unsplash.com/photo-1535591273668-578e31182c4f?w=1920') no-repeat center center fixed; background-size: cover; min-height: 100vh; }
    header { background: linear-gradient(to bottom, rgba(0,0,0,0.8), rgba(0,50,100,0.9)); color: white; padding: 40px 20px; text-align: center; border-bottom: 5px solid #ff6b00; box-shadow: 0 5px 20px rgba(0,0,0,0.5); }
    h1 { font-family: 'Pacifico', cursive; margin: 0; font-size: 3.5rem; color: #ff6b00; text-shadow: 3px 3px 6px #000; }
    .subtitle { font-size: 1.3rem; margin-top: 10px; color: #87ceeb; }
    .contenedor { max-width: 1200px; margin: 40px auto; background: rgba(255, 255, 255, 0.95); padding: 40px; border-radius: 20px; box-shadow: 0 10px 40px rgba(0,0,0,0.4); }
    h2 { color: #003366; text-align: center; font-size: 2rem; margin-bottom: 30px; border-bottom: 3px solid #ff6b00; display: inline-block; padding-bottom: 10px; }
    .grilla { display: grid; grid-template-columns: repeat(4, 1fr); gap: 25px; }
    @media (max-width: 1000px) { .grilla { grid-template-columns: repeat(2, 1fr); } }
    @media (max-width: 600px) { .grilla { grid-template-columns: 1fr; } }
    .tarjeta { border: 3px solid #003366; border-radius: 15px; padding: 15px; text-align: center; background: linear-gradient(to bottom, #ffffff, #e8f4f8); transition: transform 0.3s, box-shadow 0.3s; }
    .tarjeta:hover { transform: translateY(-10px); box-shadow: 0 15px 30px rgba(0,0,0,0.3); }
    .tarjeta img { width: 100%; height: 200px; object-fit: cover; border-radius: 10px; border: 2px solid #87ceeb; }
    .nombre { font-weight: 700; font-size: 1.2rem; margin: 15px 0; color: #003366; }
    .precio { color: #ff6b00; font-size: 1.6rem; font-weight: 700; }
    .info-contacto { text-align: center; margin-top: 40px; padding: 30px; background: linear-gradient(to right, #003366, #006699); border-radius: 15px; color: white; }
    .info-contacto h3 { font-family: 'Pacifico', cursive; font-size: 1.8rem; margin: 0 0 15px 0; color: #ff6b00; }
    .telefono { font-size: 1.5rem; font-weight: 700; color: #87ceeb; }
    .btn-actualizar { position: fixed; bottom: 20px; right: 20px; background: #ff6b00; color: white; padding: 15px 20px; border-radius: 50px; border: none; font-size: 20px; cursor: pointer; box-shadow: 0 5px 15px rgba(0,0,0,0.4); }
    .titulo-seccion { text-align: center; }
</style>
</head>
<body>

    <header>
        <h1>Provisión Silvana Pesca</h1>
        <p class="subtitle">Tudo para tu próxima aventura de pesca</p>
    </header>

    <div class="contenedor">
        <div class="titulo-seccion"><h2>Catálogo de Productos</h2></div>
        <div class="grilla" id="tienda"></div>
        
        <div class="info-contacto">
            <h3>¿Te interesa algún producto?</h3>
            <p>Contáctanos para más información o para coordinar tu compra</p>
            <p class="telefono">094 127 306</p>
        </div>
    </div>

    <button class="btn-actualizar" onclick="cargar()" title="Actualizar productos">↻</button>

    <script>
        const GIST_ID = "56e2bef40be0ea0cae53204e39ce6efc";
        const API_URL = `https://api.github.com/gists/${GIST_ID}`;

        setInterval(cargar, 10000);

        async function cargar() {
            try {
                const res = await fetch(API_URL);
                const data = await res.json();
                const productos = JSON.parse(data.files['productos.json'].content);
                
                const div = document.getElementById('tienda');
                
                if (!productos || productos.length === 0) {
                    div.innerHTML = "<p style='text-align:center; grid-column: 1/-1;'>Próximamente productos disponibles.</p>";
                    return;
                }

                div.innerHTML = "";
                productos.forEach(p => {
                    div.innerHTML += `
                        <div class="tarjeta">
                            <img src="${p.imagen}" alt="${p.nombre}">
                            <div class="nombre">${p.nombre}</div>
                            <div class="precio">$U ${p.precio}</div>
                        </div>
                    `;
                });
            } catch (error) {
                console.error('Error:', error);
            }
        }

        cargar();
    </script>
</body>
</html>
