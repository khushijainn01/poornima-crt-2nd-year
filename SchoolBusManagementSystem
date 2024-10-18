# poornima-crt-2nd-year

package com.groot.sbms;

import javax.swing.*;
import javax.swing.table.AbstractTableModel;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class SchoolBusManagementSystem {

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            try {
                UIManager.setLookAndFeel("javax.swing.plaf.nimbus.NimbusLookAndFeel");
            } catch (Exception e) {
                e.printStackTrace();
            }
            new BusManagementFrame().setVisible(true);
        });
    }
}

class BusManagementFrame extends JFrame {
    private static final long serialVersionUID = 1L;
    private CardLayout cardLayout;
    private JPanel mainPanel;

    public BusManagementFrame() {
        setTitle("School Bus Management System");
        setSize(1000, 700);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        cardLayout = new CardLayout();
        mainPanel = new JPanel(cardLayout);
        mainPanel.add(new MainMenuPanel(this), "MainMenuPanel");
        mainPanel.add(new BusManagementPanel(this), "BusManagementPanel");

        add(mainPanel);
        cardLayout.show(mainPanel, "MainMenuPanel");
    }

    public void showBusManagement() {
        cardLayout.show(mainPanel, "BusManagementPanel");
    }

    public void showMainMenu() {
        cardLayout.show(mainPanel, "MainMenuPanel");
    }
}

class MainMenuPanel extends JPanel {
    private static final long serialVersionUID = 1L;

    public MainMenuPanel(BusManagementFrame frame) {
        setLayout(new BorderLayout(10, 10));
        setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel titleLabel = new JLabel("School Bus Management System", JLabel.CENTER);
        titleLabel.setFont(new Font("Arial", Font.BOLD, 24));

        JPanel buttonPanel = new JPanel(new GridLayout(3, 1, 10, 10));
        JButton manageBusesButton = new JButton("Manage Buses");
        manageBusesButton.setFont(new Font("Arial", Font.PLAIN, 18));
        manageBusesButton.addActionListener(e -> frame.showBusManagement());
        manageBusesButton.setToolTipText("Go to the bus management section");

        JButton toggleThemeButton = new JButton("Toggle Dark Mode");
        toggleThemeButton.setFont(new Font("Arial", Font.PLAIN, 18));
        toggleThemeButton.addActionListener(new DarkModeToggleAction());

        JButton exitButton = new JButton("Exit");
        exitButton.setFont(new Font("Arial", Font.PLAIN, 18));
        exitButton.addActionListener(e -> System.exit(0));
        exitButton.setToolTipText("Exit the application");

        buttonPanel.add(manageBusesButton);
        buttonPanel.add(toggleThemeButton);
        buttonPanel.add(exitButton);

        add(titleLabel, BorderLayout.NORTH);
        add(buttonPanel, BorderLayout.CENTER);
    }
}

class BusManagementPanel extends JPanel {
    private static final long serialVersionUID = 1L;
    private ArrayList<String> buses;
    private JTextField busField;
    private DefaultListModel<String> busListModel;
    private JList<String> busList;

    public BusManagementPanel(BusManagementFrame frame) {
        buses = new ArrayList<>();
        setLayout(new BorderLayout(10, 10));
        setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));

        JLabel instructionLabel = new JLabel("Enter Bus Number:", JLabel.CENTER);
        instructionLabel.setFont(new Font("Arial", Font.PLAIN, 18));

        busField = new JTextField();
        busField.setFont(new Font("Arial", Font.PLAIN, 16));

        JPanel inputPanel = new JPanel(new BorderLayout(10, 10));
        inputPanel.add(instructionLabel, BorderLayout.NORTH);
        inputPanel.add(busField, BorderLayout.CENTER);

        JButton addBusButton = new JButton("Add Bus");
        addBusButton.setFont(new Font("Arial", Font.PLAIN, 16));
        addBusButton.addActionListener(new AddBusAction());

        JButton editBusButton = new JButton("Edit Bus");
        editBusButton.setFont(new Font("Arial", Font.PLAIN, 16));
        editBusButton.addActionListener(new EditBusAction());

        JButton removeBusButton = new JButton("Remove Bus");
        removeBusButton.setFont(new Font("Arial", Font.PLAIN, 16));
        removeBusButton.addActionListener(new RemoveBusAction());

        JButton viewBusesButton = new JButton("View Buses");
        viewBusesButton.setFont(new Font("Arial", Font.PLAIN, 16));
        viewBusesButton.addActionListener(new ViewBusesAction(frame));

        JPanel actionPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        actionPanel.add(addBusButton);
        actionPanel.add(editBusButton);
        actionPanel.add(removeBusButton);
        actionPanel.add(viewBusesButton);

        busListModel = new DefaultListModel<>();
        busList = new JList<>(busListModel);
        busList.setFont(new Font("Arial", Font.PLAIN, 16));
        JScrollPane scrollPane = new JScrollPane(busList);

        add(inputPanel, BorderLayout.NORTH);
        add(scrollPane, BorderLayout.CENTER);
        add(actionPanel, BorderLayout.SOUTH);
    }

    private class AddBusAction implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            String busNumber = busField.getText().trim();
            if (!busNumber.isEmpty()) {
                buses.add(busNumber);
                busListModel.addElement(busNumber);
                busField.setText("");
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Bus added successfully!", "Success", JOptionPane.INFORMATION_MESSAGE);
            } else {
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Please enter a valid bus number.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    private class EditBusAction implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            String busNumber = busField.getText().trim();
            int selectedIndex = busList.getSelectedIndex();

            if (selectedIndex == -1) {
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Please select a bus to edit.", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            if (!busNumber.isEmpty()) {
                buses.set(selectedIndex, busNumber); // Update bus number
                busListModel.set(selectedIndex, busNumber); // Update the list model
                busField.setText("");
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Bus updated successfully!", "Success", JOptionPane.INFORMATION_MESSAGE);
            } else {
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Please enter a valid bus number.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    private class RemoveBusAction implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            int selectedIndex = busList.getSelectedIndex();
            if (selectedIndex == -1) {
                JOptionPane.showMessageDialog(BusManagementPanel.this, "Please select a bus to remove.", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            buses.remove(selectedIndex);
            busListModel.remove(selectedIndex);
            JOptionPane.showMessageDialog(BusManagementPanel.this, "Bus removed successfully!", "Success", JOptionPane.INFORMATION_MESSAGE);
        }
    }

    private class ViewBusesAction implements ActionListener {
        private BusManagementFrame frame;

        public ViewBusesAction(BusManagementFrame frame) {
            this.frame = frame;
        }

        @Override
        public void actionPerformed(ActionEvent e) {
            if (buses.isEmpty()) {
                JOptionPane.showMessageDialog(frame, "No buses available.", "Info", JOptionPane.INFORMATION_MESSAGE);
            } else {
                StringBuilder busListString = new StringBuilder("Buses:\n");
                for (String bus : buses) {
                    busListString.append(bus).append("\n");
                }
                JOptionPane.showMessageDialog(frame, busListString.toString(), "Bus List", JOptionPane.INFORMATION_MESSAGE);
            }
        }
    }
}
