# Exemplo de como utilizar essa api no React

    import React, { useState } from 'react';
    import axios from 'axios';

    const LivroForm = () => {

        const [livro, setLivro] = useState({
            titulo: '',
            editora: '',
            preco: 0,
            paginas: 0,
            autor: '',
        });

        const handleChange = (e) => {
            const { name, value } = e.target;
            setLivro((prevLivro) => ({ ...prevLivro, [name]: value }));
        };

        const handleSubmit = async (e) => {
            e.preventDefault();

            try {
                // Faça a solicitação POST para a API
                const response = await axios.post('http://localhost:3001/livros', livro);
                console.log(response.data);
            } catch (error) {
                console.error('Erro ao cadastrar livro:', error.message);
            }
        };

        return (
            <form onSubmit={handleSubmit}>
            <label>Título:</label>
            <input type="text" name="titulo" value={livro.titulo} onChange={handleChange} />

            <label>Editora:</label>
            <input type="text" name="editora" value={livro.editora} onChange={handleChange} />

            <label>Preço:</label>
            <input type="number" name="preco" value={livro.preco} onChange={handleChange} />

            <label>Páginas:</label>
            <input type="number" name="paginas" value={livro.paginas} onChange={handleChange} />

            <label>Autor:</label>
            <input type="text" name="autor" value={livro.autor} onChange={handleChange} />

            <button type="submit">Cadastrar Livro</button>
            </form>
        );
    };

    export default LivroForm;

# Exemplo com o fetch

    const handleSubmit = async (e) => {
        e.preventDefault();
        try {
            // Faça a solicitação POST para a API usando o método fetch
            const response = await fetch('http://localhost:3001/livros', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(livro),
            });

            if (!response.ok) {
                throw new Error(`Erro na solicitação: ${response.statusText}`);
            }

            const data = await response.json();
            console.log(data);
            
        } catch (error) {
            console.error('Erro ao cadastrar livro:', error.message);
        }
    };