## Data Driven Fluid Mechanics (Notas de estudo)

### Capítulo 1
#### Cylinder Wake: Benchmark para Navier Stokes Incompressível


>  $\nabla \cdot \mathbf{u} = 0$
> 
> $\partial_t \mathbf{u} + \mathbf{u} \cdot \nabla \mathbf{u} = -\nabla p + \frac{1}{Re} \Delta \mathbf{u}$
>
> $`\Omega_{DNS} = \{ (x,y) \in \mathbb{R}: x^2 + y^2 \geq 1/4 \cap -10 \leq x \leq 40 \cap |y| \leq 10 \} `$

#### Mean Field Theory 🔍 
  > $\mathbf{u} = \mathbf{u_D} + \mathbf{u'}$
  > 
  > $\mathbf{u_D}(\mathbf{x}, t) = \mathbf{u_S}(\mathbf{x}) + a_{\Delta}(t)\mathbf{u}_{\Delta}(\mathbf{x})$
  > 
  > **Shift mode $\mathbf{u}_{\Delta}$**: 
  > $`\mathbf{u}_{\Delta} = (\mathbf{u}_0 - \mathbf{u_S}) / \lVert \mathbf{u}_0 - \mathbf{u_S} \rVert_{\Omega}`$
  > 
  > **Amplitude  $a_{\Delta}$**: 
  > $a_{\Delta} = (\mathbf{u}-\mathbf{u_S}, \mathbf{u}_{\Delta})$
  > 
  > **Fluctuation Energy $\mathcal{K}$**:
  > $`\mathcal{K} = \lVert \mathbf{u'} \rVert_{\Omega}^{2}/2`$

#### Feature Extraction 🔍
- ❓ **Proximity Maps with Classical Multidimensional Scaling (CMDS) $\gamma^m \in \mathbb{R}^2$**: Transforma features de alta dimensão em duas dimensões (Parecido com LLE)
  > $`\displaystyle E = \sum^{M}_{m=1} \sum^{M}_{n=1} [ \lVert \mathbf{u}^m -  \mathbf{u}^n \rVert - \lVert  \mathbf{\gamma}^m - \mathbf{\gamma}^n \rVert ]^2`$
  >
  > Para remover efeito translacional (centralizar o mapa):
  > 
  > $`\displaystyle \sum^{M}_{m=1} \mathbf{\gamma}^m = 0`$
  > 
  > Para remover efeito rotacional $`\mathbf{\gamma}^0`$ é tomado como o máximo

- **Manifold Extraction with Local Linear Embedding (LLE) $\gamma^m \in \mathbb{R}^N$**: Aproxima os snapshots por combinações lineares dos $K$ vizinhos próximos criano um manifold aproximado de menor dimensão
  > $`\displaystyle \mathbf{u}^m \approx \sum^{K}_{k=1} w_{mk} \mathbf{u}^{i_{k}^{m}}`$, e consequentemente $`\displaystyle \mathbf{\gamma}^m \approx \sum^{K}_{k=1} w_{mk} \mathbf{\gamma}^{i_{k}^{m}}`$
  >
  > Com $i_{k}^{m}$ sendo os indices dos $K$ vizinhos próximos e $w_{mk}$ pesos não negativos e o número de features $N$ escolhido até a convergência para o erro fixado

#### Low-Dimensional Representations (Autoencoder): Transformação do espaço de $M$ snapshots para um espaço reduzido de dimensão $N$
- **Encoder $G(\mathbf{u}^{m})$**: $`\mathbf{u}^{m} \mapsto \mathbf{a}^{m} := G(\mathbf{u}^{m})`$
- **Decoder $H(\mathbf{a}^{m})$**: $`\mathbf{a}^{m} \mapsto \mathbf{u}^{m} := H(\mathbf{a}^{m})`$
- $G$ e $H$ são escolhidos de forma a minimizar o quadrado do erro acumulado entre a aproximação e os snapshots (in-sample):
  > $`\displaystyle E_{in} = \frac{1}{M} \sum^{M}_{m=1} \lVert  \mathbf{\hat{u}}^m - \mathbf{u}^m \rVert_{\Omega}^2`$
- **Autoencoder 1 - Proper Orthogonal Decomposition (POD)**: POD é Um Autoencoder linear otimizado para encontrar subespaços otimizados
  - **POD Encoder $G$**: $`G(\mathbf{u}_{i}) = \mathbf{a}_{i} = (\mathbf{u} - \mathbf{u}_{0}, \mathbf{u}_i)_{\Omega}`$ ❓ (Não entendi o $u$ sem indice)
  - **POD Decoder $H$**: $`\displaystyle  \mathbf{\hat{u}}(\mathbf{x}) = \mathbf{u}_0(\mathbf{x}) + \sum^{M}_{i=1} \mathbf{a}_{i}\mathbf{u}_{i}(\mathbf{x})`$
- **Autoencoder 2 - K-Means**:
