Dans le cadre du projet E-Music j'ai dévellopé une base de données sur Java,

![image](https://user-images.githubusercontent.com/90392648/203002878-60afd0d6-9938-4082-bd74-eda40650ee28.png)

Son SGBD est H2, 

![H2-console](https://user-images.githubusercontent.com/90392648/203002136-fd9bd3e5-279e-44a1-875a-b09264caa671.png)

Elle est modifiables depuis H2 ou via un controlleur fait sur java,
ici se sont des controlleur qui permet a la carte d'être enregistrer

```Java

	@GetMapping("myCard/{id}")
	public String formCarteLog(ModelMap model,@AuthenticationPrincipal Parent authUSer) {
		if(authUSer.getCarte()== null) {
			Cartes cb=new Cartes();
			cb.setUser(authUSer);
			authUSer.setCarte(cb);
			carteRepo.save(cb);
		}
		
		model.put("userCo",authUSer);
		return "/user/FormCartes";
	}

	@PostMapping("myCard/edit")
	public RedirectView addCarte(ModelMap model,@AuthenticationPrincipal Parent authUSer, @ModelAttribute Cartes carte) {
		int toChange = authUSer.getCarte().getId();
		Cartes toAdd =carte;
		toAdd.setId(toChange);
		toAdd.setUser(authUSer);
		authUSer.setCarte(toAdd);
		carteRepo.save(toAdd);
		return new RedirectView("/");
	}

```
