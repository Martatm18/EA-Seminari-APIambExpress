**Enllaç del Vídeo Explicació Seminari APIambExpress:** https://drive.google.com/file/d/1m3w5nqs7owVSfk07t2EfWq53QU08NKZV/view?usp=sharing

**Referències del material consultat:**

- Apunts porporcionats pels professors
- Repositoris proporcionats pels professors
- Els vídeos proposats

**Ús de la IA**
- En aquest seminari he fet l’ús de la IA, concretament Gemini 3.6, per redactar els OPENAPI dins del fitxer Book.ts dins de routes.

**PROMPT LITERAL:** Ja tinc implementades i funcionant aquestes tres rutes de la meva API REST (Node.js, Express, TypeScript, Mongoose, Joi), amb el seu controlador i la seva validació Joi ja fets per mi:
POST /books/:bookId/tags : afegeix un tag a un llibre sense duplicar-lo
PUT /books/:bookId/tags : reemplaça tota la llista de tags d'un llibre
DELETE /books/:bookId/tags/:tag : elimina un tag d'un llibre
Necessito NOMÉS els comentaris @openapi per documentar-les a Swagger. Per a cada ruta necessito: tags: [Books], summary, description breu, parameters (bookId sempre com a path param amb el pattern d'ObjectId de Mongo, i tag com a path param al DELETE), requestBody amb el seu schema i un exemple quan la ruta porti body, i els codis de resposta 200/400/404, i 422 quan hi hagi validació de body. No necessito que toquis el controlador, el servei ni la validació Joi, que ja els tinc fets jo, només el bloc de comentaris @openapi per a cadascuna de les tres rutes. Aquí tens les meves rutes actuals:[HE ENGANXAT EL MEU FITXER DE RUTES].

**INCOHERÈNICA:** CAP

**RESPOSTA DE LA IA:** Aquí tens els tres blocs @openapi:
/**
 * @openapi
 * /books/{bookId}/tags:
 *   post:
 *     tags: [Books]
 *     summary: Añade un tag a un libro sin duplicarlo
 *     description: Si el libro ya tiene ese tag, no se repite. El tag tiene que ser uno de los permitidos.
 *     parameters:
 *       - in: path
 *         name: bookId
 *         required: true
 *         schema: { type: string, pattern: '^[0-9a-fA-F]{24}$' }
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             required: [tag]
 *             properties:
 *               tag: { type: string, example: fantasia }
 *     responses:
 *       200: { $ref: '#/components/responses/BookOne' }
 *       400: { $ref: '#/components/responses/BadRequest' }
 *       404: { $ref: '#/components/responses/NotFound' }
 *       422: { $ref: '#/components/responses/Unprocessable' }
 */

/**
 * @openapi
 * /books/{bookId}/tags:
 *   put:
 *     tags: [Books]
 *     summary: Reemplaza todos los tags de un libro
 *     description: La lista enviada sustituye a la que había. No puede tener tags repetidos.
 *     parameters:
 *       - in: path
 *         name: bookId
 *         required: true
 *         schema: { type: string, pattern: '^[0-9a-fA-F]{24}$' }
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             required: [tags]
 *             properties:
 *               tags:
 *                 type: array
 *                 items: { type: string }
 *                 example: [ciencia-ficcion, fantasia]
 *     responses:
 *       200: { $ref: '#/components/responses/BookOne' }
 *       400: { $ref: '#/components/responses/BadRequest' }
 *       404: { $ref: '#/components/responses/NotFound' }
 *       422: { $ref: '#/components/responses/Unprocessable' }
 */

/**
 * @openapi
 * /books/{bookId}/tags/{tag}:
 *   delete:
 *     tags: [Books]
 *     summary: Elimina un tag de un libro
 *     description: Si el libro no tenía ese tag, no falla y devuelve el libro igual.
 *     parameters:
 *       - in: path
 *         name: bookId
 *         required: true
 *         schema: { type: string, pattern: '^[0-9a-fA-F]{24}$' }
 *       - in: path
 *         name: tag
 *         required: true
 *         schema: { type: string }
 *         example: fantasia
 *     responses:
 *       200: { $ref: '#/components/responses/BookOne' }
 *       400: { $ref: '#/components/responses/BadRequest' }
 *       404: { $ref: '#/components/responses/NotFound' }
 */

