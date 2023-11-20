package org.example.Interfaces;

import org.example.Users.Utilisateur;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class BenevoleInterface extends JFrame {
    private JTextArea messageTextArea;
    private JTextArea requestsTextArea;
    private JTextArea statusTextArea;

    private Utilisateur utilisateur;
    public BenevoleInterface() {
        initializeUI();
    }

    public BenevoleInterface(Utilisateur utilisateur) {
        this.utilisateur = utilisateur;
        initializeUI();
    }

    private void initializeUI() {
        setTitle("Interfaz para Benevole");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(1, 3));

        // Caja para escribir sobre la ayuda que quieren dar, con nuevas cajas obligatorias
        messageTextArea = new JTextArea();
        JPanel proposePanel = new JPanel(new GridLayout(4, 1)); // Cambio en la disposición
        proposePanel.add(messageTextArea);

// Nuevas cajas obligatorias para fecha, región y descripción
        JTextField dateField = new JTextField();
        JTextField regionField = new JTextField();
        JTextField descriptionField = new JTextField();

        proposePanel.add(dateField);
        proposePanel.add(regionField);
        proposePanel.add(descriptionField);

        JScrollPane messageScrollPane = new JScrollPane(proposePanel);
        messageScrollPane.setBorder(BorderFactory.createTitledBorder("Ayuda a Ofrecer"));
        add(messageScrollPane);

        // Caja para ver las solicitudes de los demandantes
        requestsTextArea = new JTextArea();
        JScrollPane requestsScrollPane = new JScrollPane(requestsTextArea);
        requestsScrollPane.setBorder(BorderFactory.createTitledBorder("Solicitudes de Demandeur"));
        add(requestsScrollPane);

        // Caja para ver el estado de todas las ayudas propuestas
        statusTextArea = new JTextArea();
        JScrollPane statusScrollPane = new JScrollPane(statusTextArea);
        statusScrollPane.setBorder(BorderFactory.createTitledBorder("Estado de Ayudas Propuestas"));
        add(statusScrollPane);

        JButton proposeHelpButton = new JButton("Proponer Ayuda");
        proposeHelpButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // Aquí puedes agregar la lógica para procesar la ayuda propuesta
                String helpMessage = messageTextArea.getText();
                String date = dateField.getText(); // Obtener la fecha
                String region = regionField.getText(); // Obtener la región
                String description = descriptionField.getText(); // Obtener la descripción

                // Lógica para procesar la ayuda con fecha, región y descripción...
                // ...

                // Actualizar la caja de estado
                statusTextArea.append("Ayuda Propuesta: " + helpMessage + " - En Proceso\n");
            }
        });
        add(proposeHelpButton);


        //  informations de l'utilisateur pour personnaliser l'interface
        JLabel userLabel = new JLabel("Bienvenue, " + utilisateur.getNom() + " " + utilisateur.getPrenom());
        userLabel.setHorizontalAlignment(SwingConstants.CENTER);
        add(userLabel);

        setSize(800, 400);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new BenevoleInterface();
            }
        });
    }
}
