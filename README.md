# Apresentação 01/06/2026
## Exercícios aula 26

- Questão 1

Primeiramente, comecei lendo o material sobre programação concorrente da aula 26.
Após ler o material, fui fazer o primeiro exercicio. 
Eu reutilizei o código da classe de Rabbit e apenas mudei os nomes para Horse e reajustei a escrita. 
- Código da classe nova:

```hs
class Horse extends Thread {
	private String name;

	public Horse(String name) {
		this.name = name;
	}

	private void runLikeHorse() {
		System.out.println(name + " is galloping very fast");
	}

	public void run() {
		System.out.println(name + " horse is at the start of the race!");
		for (int pos = 10; pos > 0; pos--) {
			runLikeHorse();
			System.out.println(name + " is at position " + pos);
			
			// Dynamic delay for the GIF animation
			try {
				Thread.sleep(200); 
			} catch (InterruptedException e) {
				Thread.currentThread().interrupt();
			}
		}
		System.out.println(name + " horse finished the race!");
	}
}
```
Esse exercicio 1 foi bem básico e funcionou de primeira, o unico uso de IA foi para adicionar um delay para a execução dos prints para que fique melhor no gif.
<img width="1906" height="982" alt="Animação" src="https://github.com/user-attachments/assets/921fba06-67be-4dc6-abc9-1c4a499dde60" />

# Parte 2
## Código open-source concorrente.

- https://github.com/apache/commons-lang/blob/master/src/main/java/org/apache/commons/lang3/concurrent/LazyInitializer.java

A classe escolhida, LazyInitializer, serve para garantir que um objeto pesado só seja criado no momento em que for necessário, garantindo segurança quando multiplas Threads tentarem acessa-los ao mesmo tempo.

Inicialmente, ao analisar o código eu não compreendi praticamente NADA, então tive que voltar aos conceitos básicos de Threads e ai percebi que tinha muita coisa que eu não tinha entendido do conteúdo. Depois de estudar um pouco e pedir exemplos didáticos pra IA eu consegui entender melhor os Threads, ai voltei pro exercício 2. No código que escolhi tem muitas coisas ainda que não consigo entender pra que serve, como o uso de volatile e métodos que nunca ouvi falar. No entanto acho que entendi boa parte da parte principal do código que é pra bloquear o acesso de diversas Threads a um objeto nulo através do uso de synchronized.

```hs
// Código simplificado para a apresentação
public abstract class LazyInitializer<T> {

    private volatile T object;

    public T get() throws ConcurrentException {
        // Primeira checagem (sem sincronização para ser rápido)
        T result = object;

        if (result == null) {
            // Se estiver nulo, bloqueia o bloco para que apenas UMA thread por vez entre aqui
            synchronized (this) {
                result = object;
                // Segunda checagem (agora protegida) para garantir que outra thread não criou o objeto antes
                if (result == null) {
                    object = result = initialize();
                }
            }
        }

        return result;
    }

    // Método que o desenvolvedor deve sobrescrever para criar o objeto pesado
    protected abstract T initialize() throws ConcurrentException;
}
```
