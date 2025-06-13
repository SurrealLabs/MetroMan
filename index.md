<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página Principal</title>
    <style>
        /* Button CSS - Preserving your original button style */
        .button-82-pushable {
            position: relative;
            border: none;
            background: transparent;
            padding: 0;
            cursor: pointer;
            outline-offset: 4px;
            transition: filter 250ms;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
            margin: 20px 0;
        }

        .button-82-shadow {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 12px;
            background: hsl(0deg 0% 0% / 0.25);
            will-change: transform;
            transform: translateY(2px);
            transition: transform 600ms cubic-bezier(.3, .7, .4, 1);
        }

        .button-82-edge {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 12px;
            background: linear-gradient(
                to left,
                hsl(340deg 100% 16%) 0%,
                hsl(340deg 100% 32%) 8%,
                hsl(340deg 100% 32%) 92%,
                hsl(340deg 100% 16%) 100%
            );
        }

        .button-82-front {
            display: block;
            position: relative;
            padding: 12px 27px;
            border-radius: 12px;
            font-size: 1.1rem;
            color: white;
            background: hsl(345deg 100% 47%);
            will-change: transform;
            transform: translateY(-4px);
            transition: transform 600ms cubic-bezier(.3, .7, .4, 1);
        }

        .button-82-pushable:hover {
            filter: brightness(110%);
        }

        .button-82-pushable:hover .button-82-front {
            transform: translateY(-6px);
            transition: transform 250ms cubic-bezier(.3, .7, .4, 1.5);
        }

        .button-82-pushable:active .button-82-front {
            transform: translateY(-2px);
            transition: transform 34ms;
        }

        .button-82-pushable:hover .button-82-shadow {
            transform: translateY(4px);
            transition: transform 250ms cubic-bezier(.3, .7, .4, 1.5);
        }

        .button-82-pushable:active .button-82-shadow {
            transform: translateY(1px);
            transition: transform 34ms;
        }

        .button-82-pushable:focus:not(:focus-visible) {
            outline: none;
        }

        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            color: #333;
        }

        h1 {
            color: #444;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }

        a {
            color: #d00;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <button class="button-82-pushable" role="button" onclick="location.href='balkeon'">
        <span class="button-82-shadow"></span>
        <span class="button-82-edge"></span>
        <span class="button-82-front text">
            Aprende Balkeon
        </span>
    </button>

    <h1>Red de Comunidad del Metro de Santiago <a href="https://www.metroman.me/comunidades/comunidad-metro-de-santiago/">aquí</a></h1>

    <h1>¿Quién soy?</h1>
    <p>Hola! Soy Metroman, empecé en 2020 con esta tal identidad en Internet, todo inició con la iniciativa de construir el Metro en BTE Chile cuando portaba uno de mis miles nombres "FGY Games", gracias a un compañero (actualmente inactivo) de ese servidor de Discord terminé adoptando mi nombre definitivo: MetroMan. No me pregunten si existirán problemas de CopyRight, ni yo sé, pero actualmente me estoy dedicando a ordenar mi vida preparándome para lo que quizás sea mi futuro: Redes Sociales y Traducción. Por eso aquí tienen una versión mejorada de mi antigua página web, con dominio personalizado y todo.</p>

    <p>Expulsado de BTE Chile durante Noviembre 2024, pronto comentaré qué haré ahora con mis Redes Sociales, por mientras estoy armando un Conlang en un Servidor de Discord: <a href="https://discord.gg/8NPsyq7rp7">Aquí puedes Entrar</a></p>

    <p>Página en construcción</p>
</body>
</html>
