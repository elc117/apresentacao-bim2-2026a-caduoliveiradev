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
```
		System.out.println(name + " horse finished the race!");
	}
}
```
Esse exercicio 1 foi bem básico e funcionou de primeira, o unico uso de IA foi para adicionar um delay para a execução dos prints para que fique melhor no gif.
