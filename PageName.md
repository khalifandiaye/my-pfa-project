public class Calculette extends JFrame {
> private JPanel container = new JPanel();
> //Tableau stockant les éléments à afficher dans la calculatrice
> String[.md](.md) tab\_string = {"1", "2", "3", "4", "5", "6", "7", "8", "9", "0", ".", "=", "C", "+", "-", "**", "/"};
> //Un bouton par élément à afficher
> JButton[.md](.md) tab\_button = new JButton[tab\_string.length];
> private JLabel ecran = new JLabel("0");
> private Dimension dim = new Dimension(50, 40);
> private Dimension dim2 = new Dimension(50, 31);
> private double chiffre1;
> private boolean clicOperateur = false, update = false;
> private String operateur = "";**

> public Calculette(){
> > this.setSize(240, 260);
> > this.setTitle("Calculette");
> > this.setDefaultCloseOperation(JFrame.EXIT\_ON\_CLOSE);
> > this.setLocationRelativeTo(null);
> > this.setResizable(false);
> > //On initialise le conteneur avec tous les composants
> > initComposant();
> > //On ajoute le conteneur
> > > this.setContentPane(container);
> > > this.setVisible(true);

> }

> private void initComposant(){
> > //On définit la police d'écriture à utiliser
> > Font police = new Font("Arial", Font.BOLD, 20);
> > // ecran = new JLabel("0");
> > > ecran.setFont(police);
> > > //On aligne les informations à droite dans le JLabel
> > > ecran.setHorizontalAlignment(JLabel.RIGHT);
> > > ecran.setPreferredSize(new Dimension(220, 20));
> > > JPanel operateur = new JPanel();
> > > operateur.setPreferredSize(new Dimension(55, 225));
> > > JPanel chiffre = new JPanel();
> > > chiffre.setPreferredSize(new Dimension(165, 225));
> > > JPanel panEcran = new JPanel();
> > > panEcran.setPreferredSize(new Dimension(220, 30));


> //On parcourt le tableau initialisé
> //afin de créer nos boutons
> for(int i = 0; i < tab\_string.length; i++){
> > tab\_button[i](i.md) = new JButton(tab\_string[i](i.md));
> > tab\_button[i](i.md).setPreferredSize(dim);
> > switch(i){
> > > //Pour chaque élément situé à la fin du tableau
> > > //et qui n'est pas un chiffre
> > > //on définit le comportement à avoir grâce à un listener
> > > case 11 :
> > > > tab\_button[i](i.md).addActionListener(new EgalListener());
> > > > chiffre.add(tab\_button[i](i.md));
> > > > break;

> > > case 12 :
> > > > tab\_button[i](i.md).setForeground(Color.red);
> > > > tab\_button[i](i.md).addActionListener(new ResetListener());
> > > > operateur.add(tab\_button[i](i.md));
> > > > break;

> > > case 13 :
> > > > tab\_button[i](i.md).addActionListener(new PlusListener());
> > > > tab\_button[i](i.md).setPreferredSize(dim2);
> > > > operateur.add(tab\_button[i](i.md));
> > > > break;

> > > case 14 :
> > > > tab\_button[i](i.md).addActionListener(new MoinsListener());
> > > > tab\_button[i](i.md).setPreferredSize(dim2);
> > > > operateur.add(tab\_button[i](i.md));
> > > > break;

> > > case 15 :
> > > > tab\_button[i](i.md).addActionListener(new MultiListener());
> > > > tab\_button[i](i.md).setPreferredSize(dim2);
> > > > operateur.add(tab\_button[i](i.md));
> > > > break;

> > > case 16 :
> > > > tab\_button[i](i.md).addActionListener(new DivListener());
> > > > tab\_button[i](i.md).setPreferredSize(dim2);
> > > > operateur.add(tab\_button[i](i.md));
> > > > break;

> > > default :
> > > > //Par défaut, ce sont les premiers éléments du tableau
> > > > //donc des chiffres, on affecte alors le bon listener
> > > > chiffre.add(tab\_button[i](i.md));
> > > > tab\_button[i](i.md).addActionListener(new ChiffreListener());
> > > > break;

> > }

> }
> panEcran.add(ecran);
> panEcran.setBorder(BorderFactory.createLineBorder(Color.black));
> container.add(panEcran, BorderLayout.NORTH);
> container.add(chiffre, BorderLayout.CENTER);
> container.add(operateur, BorderLayout.EAST);
> }

> //Méthode permettant d'effectuer un calcul selon l'opérateur sélectionné
> private void calcul(){
> > if(operateur.equals("+")){
> > > chiffre1 = chiffre1 +
> > > > Double.valueOf(ecran.getText()).doubleValue();

> > > ecran.setText(String.valueOf(chiffre1));

> > }
> > if(operateur.equals("-")){
> > > chiffre1 = chiffre1 -
> > > > Double.valueOf(ecran.getText()).doubleValue();

> > > ecran.setText(String.valueOf(chiffre1));

> > }
> > if(operateur.equals("**")){
> > > chiffre1 = chiffre1**
> > > > Double.valueOf(ecran.getText()).doubleValue();

> > > ecran.setText(String.valueOf(chiffre1));

> > }
> > if(operateur.equals("/")){
> > > try{
> > > > chiffre1 = chiffre1 /
> > > > > Double.valueOf(ecran.getText()).doubleValue();

> > > > ecran.setText(String.valueOf(chiffre1));

> > > } catch(ArithmeticException e) {
> > > > ecran.setText("0");

> > > }

> > }

> }

> //Listener utilisé pour les chiffres
> //Permet de stocker les chiffres et de les afficher
> class ChiffreListener implements ActionListener {
> > public void actionPerformed(ActionEvent e){
> > > //On affiche le chiffre additionnel dans le label
> > > String str = ((JButton)e.getSource()).getText();
> > > if(update){
> > > > update = false;

> > > }
> > > else{
> > > > if(!ecran.getText().equals("0"))
> > > > > str = ecran.getText() + str;

> > > }
> > > ecran.setText(str);

> > }

> }

> //Listener affecté au bouton =
> class EgalListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > calcul();
> > > update = true;
> > > clicOperateur = false;

> > }

> }

> //Listener affecté au bouton +
> class PlusListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > if(clicOperateur){
> > > > calcul();
> > > > ecran.setText(String.valueOf(chiffre1));

> > > }
> > > else{
> > > > chiffre1 = Double.valueOf(ecran.getText()).doubleValue();
> > > > clicOperateur = true;

> > > }
> > > operateur = "+";
> > > update = true;

> > }

> }

> //Listener affecté au bouton -
> class MoinsListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > if(clicOperateur){
> > > > calcul();
> > > > ecran.setText(String.valueOf(chiffre1));

> > > }
> > > else{
> > > > chiffre1 = Double.valueOf(ecran.getText()).doubleValue();
> > > > clicOperateur = true;

> > > }
> > > operateur = "-";
> > > update = true;

> > }

> }

> //Listener affecté au bouton **> class MultiListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > if(clicOperateur){
> > > > calcul();
> > > > ecran.setText(String.valueOf(chiffre1));

> > > }
> > > else{
> > > > chiffre1 = Double.valueOf(ecran.getText()).doubleValue();
> > > > clicOperateur = true;

> > > }
> > > operateur = "**";
> > > update = true;

> > }

> }

> //Listener affecté au bouton /
> class DivListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > if(clicOperateur){
> > > > calcul();
> > > > ecran.setText(String.valueOf(chiffre1));

> > > }
> > > else{
> > > > chiffre1 = Double.valueOf(ecran.getText()).doubleValue();
> > > > clicOperateur = true;

> > > }
> > > operateur = "/";
> > > update = true;

> > }

> }

> //Listener affecté au bouton de remise à zéro
> class ResetListener implements ActionListener {
> > public void actionPerformed(ActionEvent arg0){
> > > clicOperateur = false;
> > > update = true;
> > > chiffre1 = 0;
> > > operateur = "";
> > > ecran.setText("");

> > }

> }
}



> class Main {
> > public static void main(String[.md](.md) args) {
> > > Calculette calculette = new Calculette();

> > }
}