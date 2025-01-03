/ Restaurant Reservation App using React Native

import React, { useState } from 'react';
import { View, Text, FlatList, TouchableOpacity, StyleSheet, Alert, Image } from 'react-native';

const App = () => {
  // Sample data for restaurants
  const restaurants = [
    { id: '1', name: 'Italian Cuisine' },
    { id: '2', name: 'Indian Spice' },
  ];

  const [bookings, setBookings] = useState([]);

  const handleBooking = (restaurantName) => {
    const newBooking = { id: Date.now().toString(), name: restaurantName };
    setBookings([...bookings, newBooking]);
    Alert.alert('Booking Confirmed', `You booked ${restaurantName}`);
  };

  const handleEditBooking = (bookingId) => {
    Alert.prompt(
      'Edit Booking',
      'Enter new restaurant name:',
      [
        {
          text: 'Cancel',
          style: 'cancel',
        },
        {
          text: 'OK',
          onPress: (newName) => {
            setBookings((prevBookings) =>
              prevBookings.map((booking) =>
                booking.id === bookingId ? { ...booking, name: newName } : booking
              )
            );
          },
        },
      ]
    );
  };

  const handleDeleteBooking = (bookingId) => {
    setBookings((prevBookings) => prevBookings.filter((booking) => booking.id !== bookingId));
    Alert.alert('Booking Deleted', 'Your booking has been removed.');
  };

  return (
    <View style={styles.container}>
      <View style={styles.logoContainer}>
        <Image source={require('./assets/club_aqua_park.jpg')} style={styles.logo} />
      </View>
      <Text style={styles.title}>Hotel Restaurant Booking</Text>
      <Text style={styles.subtitle}>Select a Restaurant to Book:</Text>
      <FlatList
        data={restaurants}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity
            style={styles.restaurantButton}
            onPress={() => handleBooking(item.name)}
          >
            <Text style={styles.restaurantText}>{item.name}</Text>
          </TouchableOpacity>
        )}
      />

      <Text style={styles.subtitle}>Your Bookings:</Text>
      <FlatList
        data={bookings}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <View style={styles.bookingItem}>
            <Text style={styles.bookingText}>{item.name}</Text>
            <View style={styles.bookingActions}>
              <TouchableOpacity
                style={styles.editButton}
                onPress={() => handleEditBooking(item.id)}
              >
                <Text style={styles.actionText}>Edit</Text>
              </TouchableOpacity>
              <TouchableOpacity
                style={styles.deleteButton}
                onPress={() => handleDeleteBooking(item.id)}
              >
                <Text style={styles.actionText}>Delete</Text>
              </TouchableOpacity>
            </View>
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff8e1',
  },
  logoContainer: {
    alignItems: 'center',
    marginBottom: 20,
  },
  logo: {
    width: 150,
    height: 150,
    resizeMode: 'contain',
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    marginBottom: 20,
    textAlign: 'center',
    color: '#ff7043',
  },
  subtitle: {
    fontSize: 20,
    fontWeight: 'bold',
    marginVertical: 10,
    color: '#ff9800',
  },
  restaurantButton: {
    padding: 15,
    marginVertical: 10,
    backgroundColor: '#4caf50',
    borderRadius: 8,
  },
  restaurantText: {
    color: '#fff',
    fontSize: 18,
    textAlign: 'center',
  },
  bookingItem: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    padding: 15,
    marginVertical: 10,
    backgroundColor: '#fff3e0',
    borderRadius: 8,
  },
  bookingText: {
    fontSize: 16,
  },
  bookingActions: {
    flexDirection: 'row',
  },
  editButton: {
    marginRight: 10,
    padding: 5,
    backgroundColor: '#ffa726',
    borderRadius: 5,
  },
  deleteButton: {
    padding: 5,
    backgroundColor: '#e53935',
    borderRadius: 5,
  },
  actionText: {
    color: '#fff',
  },
});

export default App;
# Mostafa
BUTTLER
